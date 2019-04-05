# The Foreman Release Engineering scripts

These are the scripts I use while releasing [The Foreman](https://theforeman.org). They automate most of the [release process](https://github.com/theforeman/tool_belt/blob/master/procedures/foreman/release.md.erb).

## Typical non-RC1 flow:

Make sure `VERSION` is correct in `settings` and `FULLVERSION` in `releases/$VERSION/settings`.

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
