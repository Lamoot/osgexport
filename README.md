# OpenMW OSGT exporter for Blender

OpenMW OSGT exporter for [Blender](https://www.blender.org), making the
format viable for importing meshes into [OpenMW](https://openmw.org)
using a libre format.

This is a fork of the [Blender OpenSceneGraph Exporter](https://github.com/cedricpinson/osgexport/) updated for 2.80+ Blender versions and
adjusted to support the specifics of Blender to OpenMW asset pipeline.

## Installation (Blender 2.8+)

1. Copy the `osg` directory to the location where Blender stores the
   scripts/addons folder on your system (you should see other io_scene_*
   folders there from other addons). Copy the entire dir and not just its
   contents.
2. Go to the Blender settings and enable the "OpenMW Native" addon.

## Command line usage

`osgexport` needs to inject the path to exporter modules into PYTHONPATH. The injection is done by reading the value of the `BlenderExporter` environment variable (see [\_\_init\_\_.py](https://github.com/cedricpinson/osgexport/blob/master/exporter/osg/__init__.py#L46-51)).

```shell

$ BlenderExporter="/path-to-osgexport/blender-2.5/exporter" \
    blender -b "input.blend" \
    -P "${BlenderExporter}/osg/__init__.py" \
    -- --output="output.osgt" \
    [--apply-modifiers] [--enable-animation] [--json-materials] [--enable-animation] \
    [--bake-all] [--bake-quaternions]
```
## Tests

To run tests:

```shell

mkdir tests && cd tests
cmake ../ -DBLENDER:FILEPATH="/my/path/to/blender" -DTEST=ON
make  # runs test building osgt files for models in blender-2.xx/data/
make test  # runs python test located in blender-2.xx/test/

```

To troubleshoot python tests:  `ctest --debug` or `ctest --output-on-failure`
