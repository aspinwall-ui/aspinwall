pkgdatadir = join_paths(get_option('prefix'), get_option('datadir'), meson.project_name())
submoduledir = join_paths(pkgdatadir, 'aspinwall', 'launcher')
gnome = import('gnome')

gnome.compile_resources('aspinwall.launcher',
  join_paths('ui', 'aspinwall.launcher.gresource.xml'),
  gresource_bundle: true,
  install: true,
  install_dir: pkgdatadir,
)

python = import('python')

conf = configuration_data()
conf.set('PYTHON', python.find_installation('python3').path())
conf.set('VERSION', meson.project_version())
conf.set('localedir', join_paths(get_option('prefix'), get_option('localedir')))
conf.set('pkgdatadir', pkgdatadir)

configure_file(
  input: 'aspinwall-launcher.in',
  output: 'aspinwall-launcher',
  configuration: conf,
  install: true,
  install_dir: get_option('bindir')
)

launcher_sources = [
  '__init__.py',
  'about.py',
  'app_chooser.py',
  'config.py',
  'clockbox.py',
  'settings.py',
  'wallpaper.py',
  'widget_chooser.py',
  'widgetbox.py',
  'widgetview.py',
  'widgetmanager.py',
  'window.py',
]

install_data(launcher_sources, install_dir: submoduledir)

subdir('ui')
