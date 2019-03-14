# ModuleSync Configs

Module sync configurations for Vision-IT Modules

## How to use it

```bash
git clone https://github.com/vision-it/modulesync_configs.git
cd modulesync_config
bundle install --path=.bundle
bundle exec msync help update
```

## Examples

### module sync one specific module

```bash
bundle exec msync update -f {module_name} --message "modulesync {git-tag}"
```

### module sync one module and review changes before submitting changes

```bash
bundle exec msync update -f {module_name} --noop
cd modules/{module_name}
# edit then git commit/push
```

### Syncing all modules

This will sync everything in the `managed_modules.yml`

```bash
bundle exec msync update --message "modulesync $(date +%Y-%m-%d)"
```

### Clean up old mess before syncing

```bash
find modules/* -maxdepth 0 -type d | while read module; do
  cd $module
  git status
  git checkout master
  git pull
  git fetch origin --prune
  git branch -d modulesync
  cd ..
  cd ..
done
```
