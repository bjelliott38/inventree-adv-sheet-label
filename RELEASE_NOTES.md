# v1.4.0 Release Notes

This release packages the working sheet-printing configuration into a clean production state.

## Files to replace in the fork

Copy these files into the existing repository:

- `advanced_sheet_label/printing_plugin.py`
- `advanced_sheet_label/layouts.py`
- `CHANGELOG.md`

The `printing_plugin.py` in this release intentionally does **not** contain the temporary
`plugin_debug` directory creation or raw HTML dump code used during troubleshooting.

## Repository structure

Keep the existing upstream repository structure. The relevant portion should look like:

```text
inventree-adv-sheet-label/
├── advanced_sheet_label/
│   ├── __init__.py
│   ├── printing_plugin.py
│   ├── layouts.py
│   └── ... existing plugin files ...
├── CHANGELOG.md
├── README.md
├── LICENSE
└── pyproject.toml
```

Do not rename the package directory. In the installed InvenTree container it is imported as:

`advanced_sheet_label`

## Version

`AdvancedLabelSheet.VERSION` is set to `1.4.0`.

If `pyproject.toml` also declares a package version, update that version to `1.4.0` before tagging.

## Git commands

From the root of the fork:

```bash
git checkout -b release/v1.4.0

# Copy the supplied files into the repository, then:
git add advanced_sheet_label/printing_plugin.py
git add advanced_sheet_label/layouts.py
git add CHANGELOG.md

# If pyproject.toml contains a package version, edit it to 1.4.0 and:
git add pyproject.toml

git commit -m "Release v1.4.0: Avery layouts and production cleanup"
git push -u origin release/v1.4.0
```

After final testing / merging to `main`:

```bash
git checkout main
git pull
git tag -a v1.4.0 -m "AdvancedLabelSheet v1.4.0"
git push origin v1.4.0
```

## Reinstall from the fork

After the v1.4.0 changes are on the branch / tag used by InvenTree:

```bash
docker exec --user root inventree-inventree-server-1 \
  pip install --force-reinstall --no-cache-dir \
  "git+https://github.com/bjelliott38/inventree-adv-sheet-label.git@v1.4.0"

docker exec --user root inventree-worker \
  pip install --force-reinstall --no-cache-dir \
  "git+https://github.com/bjelliott38/inventree-adv-sheet-label.git@v1.4.0"

docker restart inventree-inventree-server-1 inventree-worker
```

Verify:

```bash
docker exec inventree-inventree-server-1 pip freeze | grep -i sheet-label
```

## Layout validation status

- Avery 5163: validated with multiple selected parts.
- Avery Presta 94220: definition included; perform one alignment test sheet.
- Avery 22806: definition included; perform one alignment test sheet.
