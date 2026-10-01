# Changelog

## 2.5.4 - Oct 01, 2026

### Metadata Updates

- Updated the WordPress plugin header `Plugin URI` to point to the Kane Brands GitHub repository.
- Updated the displayed plugin author to Kane Brands with the Kane Brands GitHub profile as the author URL.
- Updated the plugin update-details author response to link to Kane Brands.
- Added README credit for original author Matthew Muro and the original Visual Form Builder Pro site.
- Updated the WordPress readme stable tag and release notes for version 2.5.4.

## PHP 8.3 Modernization Commit

This commit updates the legacy Visual Form Builder Pro PHP code so it can run more cleanly on PHP 8.3 and newer while preserving the original plugin behavior.

### Compatibility Updates

- Added PHP 8.x compatibility attributes for legacy classes that may use dynamic properties.
- Added `#[ReturnTypeWillChange]` to legacy `ArrayAccess`, `Iterator`, and `Countable` implementations to prevent interface signature deprecation notices.
- Replaced deprecated `strftime()` usage with `date()` for Excel XML export date formatting.
- Replaced deprecated `utf8_encode()` usage with safer conversion paths using `mb_convert_encoding()`, `iconv()`, or WordPress UTF-8 validation fallback.
- Fixed method signatures where optional parameters were declared before required parameters, which PHP 8.3 reports as deprecated.

### Serialized Data Handling

- Added shared helpers for safer unserialization of legacy stored plugin data.
- Updated direct `unserialize()` calls in runtime paths to use safer helpers or WordPress-compatible handling.
- Preserved support for legacy comma-separated recipient lists where older data may not be serialized.
- Added fallbacks for malformed or empty serialized settings so invalid saved data does not produce PHP warnings before the plugin can recover.
- Updated entry-detail repair flow to avoid native unserialize warnings while preserving the existing truncated-data repair behavior.

### Session Handling

- Hardened legacy session cookie parsing so malformed session cookies do not produce undefined-offset notices.
- Added a public session ID getter to the database-backed session class.
- Updated the session wrapper to use the getter instead of accessing a protected property directly.
- Preserved the existing optional PHP session mode controlled by `VFB_USE_PHP_SESSIONS`.

### Request and Server Guards

- Added guards around optional front-end request fields used by reCAPTCHA validation.
- Added guards around server variables such as remote address, user agent, referrer, and server name to avoid notices in unusual server environments.
- Normalized invalid email-rule and conditional-rule data to arrays before counting or iterating over it.
- Normalized Akismet metadata before iterating over it.

### Export and Admin Stability

- Updated export email-recipient handling so invalid or legacy stored recipient values do not cause warnings.
- Updated PayPal price-field and form option handling to use safer legacy-data parsing.
- Updated email design loading to handle missing or malformed saved design data.
- Updated field option loading in admin and front-end output paths where direct unserialization could warn on invalid values.

### Validation Performed

- Ran PHP 8.3.35 lint checks across all PHP files in the repository.
- Confirmed all PHP files report no syntax errors.
- Confirmed the final lint pass reports no PHP 8.3 lint-time deprecation output.

### Follow-Up Testing Recommended

- Activate the plugin in a WordPress environment running PHP 8.3 or newer.
- Create, edit, copy, trash, restore, and delete forms.
- Submit forms with each supported field type.
- Test email notifications and autoresponders.
- Test conditional fields and email rules.
- Test entry viewing, editing, spam handling, and export formats.
- Test configured integrations such as reCAPTCHA, Akismet, PayPal, and any installed add-ons.
