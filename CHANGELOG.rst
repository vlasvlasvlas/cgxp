This file includes migration steps for each release of CGXP.


Version 1.6
===========

1. GeoMapFish 1.6 uses MapFishPrint version 3. In the configuration of the
   `cgxp_print` plugin, `fields` is deprecated and should be replaced by
   `additionalAttributes`. By the way the fields ('title' and 'comments')
   are no longer provided by default and must be described (and translated)
   in the ``additionalAttributes`` param.

2. Autoprojection capabilities:

    The property ``projectionCode`` of FullTextSearch plugin is shifted
    in the MapPanel. For keeping the ability to enter inversed coordinates
    in the FTS, the MapPanel must owns an appropriate property ``restrictedExtent``.


Version 1.5
===========

1. In the configuration of ``CGXP/widgets/tree/LayerTree.js`` rename `frienlyUrl`
   to `friendlyUrl`.

2. In ``CGXP/plugins/LayerTree.js`` (``ptype: "cgxp_layertree"``),
   parameters ``themes``, ``uniqueTheme``, ``permalinkThemes``,
   ``defaultThemes``, ``wmsURL`` have been moved to the output
   widget. As a result they must be encapsulated into an ``outputConfig``
   object in the plugin configuration.

3. Editing plugin variable name change:

    The variable `windowOptions` of the plugin Editing is now named `attributesWindowOptions`,
    modify your Editing plugin config in the edit.js accordingly.


Version 1.4.4
=============

1. In the ``CGXP/plugins/ContextualData.js`` fix the typo from `wsg` to `wgs`,
   used in the `tpls` attribute.


Version 1.4
===========

1. Rename ``CGXP/plugins/FeatureGrid.js`` to ``CGXP/plugins/FeaturesGrid.js``
   (present in ``jsbuild/app.cfg``) and its ``ptype`` from
   ``cgxp_featuregrid`` to ``cgxp_featuresgrid`` (present in the ``viewer.js``)
   for name consistency.

2. Add new ``themes`` argument to the plugin ``cgxp_featuresgrid`` to be able to
   display the Identifier Attribute on the drawn features.

3. Refactor ``CGXP/plugins/FullTextSearch.js`` into a plugin and widget
   ``CGXP/widgets/FullTextSearch.js``.  Configuration of the plugin has changed,
   now there is widgetOptions for configuration of the widget.


Version 1.3.4
=============

1. Patch OpenLayers in the camptocamp repository,
   don't miss to do `git submodule sync`.


Version 1.3
===========

1. For consistency reasons, plugins with action configuration have been modified
   to rename their ``options`` parameter to ``actionConfig``. Please make sure
   to update your plugins configurations accordingly.

2. Former CGXP plugin ``SwitchableWMTSSource`` has been removed and replaced by
   an OpenLayers addin, ``OpenLayers.Layer.SwitchableWMTS``, combined to a
   standard ``OLSource``. Here is an example of the new syntax to use:

   .. code:: javascript

       {
           source: "olsource",
           type: "OpenLayers.Layer.SwitchableWMTS",
           group: 'background',
           args: [Ext.applyIf({
               name: OpenLayers.i18n('relief'),
               mapserverLayers: 'relief_raster',
               queryLayers: [],
               zoomThreshold: 11,
               ref: 'relief',
               layer: 'dtm_av_relief_02m',
               params:  {'time': '200703'},
               group: 'background'
           }, WMTS_OPTIONS)]
       }
