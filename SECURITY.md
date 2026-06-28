# Security Policy

## Supported Versions

This is a static browser game prototype. The latest `main` branch is the only supported version.

## Reporting Issues

If you find a security issue, do not open a public issue with exploit details.

Contact the repository owner privately through GitHub profile/contact channels.

## Security Notes

The game is designed to be static:

- no backend
- no login
- no cookies required
- no database
- no external API calls
- no npm dependencies

This greatly reduces attack surface.

## Things to Avoid

Do not add:

- analytics scripts
- ad scripts
- third-party CDN dependencies
- tracking pixels
- remote configuration
- secret keys
- API tokens
- backend credentials
