# The Foreman Release Engineering scripts

These are the scripts I use while releasing [The Foreman](https://theforeman.org). They automate most of the [release process](https://github.com/theforeman/tool_belt/blob/master/procedures/foreman/release.md.erb).

## Typical release flow

Make sure `VERSION` is correct in `settings` and `FULLVERSION` in `releases/$VERSION/settings`. This assumes a GPG key is already present.

```bash
./tag_project
./release_tarballs
./download_tarballs
./inspect_tarballs
./sign_tarballs
./bump_deb_packaging
./bump_rpm_packaging
./release_packages
# These steps can happen during the build after RPMs have been built but DEBs are still running
./download_rpms
./sign_rpms
./upload_rpm_signatures
./upload_rpms
./process_rpms
```

## GPG keys

This assumes [gopass](https://github.com/gopasspw/gopass) is already set up.

### Generating for a new release

When starting a new release, the following scripts can be used to generate a new key:

```bash
generate_gpg
# Now set GPGKEY and FULLGPGKEY in releases/$VERSION/settings
export_gpg_private
export_gpg_public
sign_gpg
upload_gpg
```

### Importing an existing release

When a key has already been generated, it can be imported from the backups:

```bash
import_gpg_private
```
