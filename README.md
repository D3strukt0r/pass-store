# pass-store

My personal password store, encrypted with [pass](https://www.passwordstore.org/).

[![License](https://img.shields.io/github/license/d3strukt0r/pass-store?label=License)](LICENSE.txt)
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.0-4baaaa)][code-of-conduct]

## Layout

- `*.gpg` — encrypted password entries. Directories are categories (e.g. `web/github.com.gpg`).
- `.gpg-id` — GPG key ID(s) authorized to decrypt entries in this store.
- `docker-credential-helpers/` — data directory for [`docker-credential-pass`](https://github.com/docker/docker-credential-helpers), Docker's pass-backed credential helper.

## Prerequisites

- [`pass`](https://www.passwordstore.org/) (or [`gopass`](https://www.gopass.pw/))
- [GnuPG](https://gnupg.org/)
- The private GPG key matching `.gpg-id`

## Restoring on a new machine

The store must live at pass's default path so that `pass`, [browserpass-native](https://github.com/browserpass/browserpass-native?tab=readme-ov-file#install-on-windows), and similar tools find it without extra configuration.

### Linux / macOS

```sh
git clone git@github.com:D3strukt0r/pass-store.git ~/.password-store
```

### Windows

```powershell
git clone git@github.com:D3strukt0r/pass-store.git $env:USERPROFILE\.password-store
```

This places the store at `C:\Users\<user>\.password-store`, which is the path [browserpass-native's Windows install guide](https://github.com/browserpass/browserpass-native?tab=readme-ov-file#install-on-windows) expects by default.

### Import the GPG key and verify

```sh
gpg --import private.key
pass ls
```

## Integrations

### browserpass

[browserpass](https://github.com/browserpass/browserpass-extension) (Firefox / Chrome) plus [browserpass-native](https://github.com/browserpass/browserpass-native) read entries from this store directly. With the store at the default path above, no additional configuration is needed.

### docker-credential-pass

[`docker-credential-pass`](https://github.com/docker/docker-credential-helpers) stores Docker registry credentials as `pass` entries under `docker-credential-helpers/`. Set `"credsStore": "pass"` in `~/.docker/config.json` to enable it.

## Contributing

Please read [CONTRIBUTING.md][contributing] for details on our code of conduct and the process for submitting pull requests.

This project uses [Conventional Commits](https://www.conventionalcommits.org/).

## Authors

### Special thanks for all the people who had helped this project so far

- **Manuele** - [D3strukt0r](https://github.com/D3strukt0r)

See also the full list of [contributors][gh-contributors] who participated in this project.

### I would like to join this list. How can I help the project?

We're currently looking for contributions for the following:

- [ ] Bug fixes
- [ ] Translations
- [ ] etc...

For more information, please refer to our [CONTRIBUTING.md][contributing] guide.

## License

This project is licensed under the MIT License - see the [LICENSE.txt](LICENSE.txt) file for details.

## Acknowledgments

This project currently uses no third-party libraries or copied code.

[gh-contributors]: https://github.com/D3strukt0r/pass-store/contributors
[contributing]: https://github.com/D3strukt0r/.github/blob/master/CONTRIBUTING.md
[code-of-conduct]: https://github.com/D3strukt0r/.github/blob/master/CODE_OF_CONDUCT.md
