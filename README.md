TileMill
--------
TileMill is a map style editor and simple data visualization tool. It currently
provides

- management of layers with shapefile-based datasources and stylesheets in a
Mapnik/Cascadenik MML file,
- an interface for editing Mapnik/Cascadenik MSS files,
- inspection of metadata in datasources including field data types, sample
values, and so on,
- a set of sensible visualization tools for labeling and shading maps to quickly
explore a datasource.


Architecture
------------
TileMill is based on [TileLive](http://github.com/developmentseed/TileLive) and
follows its lead by making the interaction between the map storage backend, map
editing client, and map rasterizer/inspector RESTful. A typical TileMill
installation thus divides its tasks into three separate components:

- The TileMill client consists of HTML and JavaScript that provides the editing
and visualization interface that users interact with.
- The TileMill server provides the storage and retrieval mechanism for the MML
and MSS files that the client creates and edits. The TileMill server **must** be
accessible via HTTP to both the TileMill client and the rasterizer.
- The rasterizer (in this case TileLiteLive) renders maps based on the data
sources and styles described by MML files on the TileMill server. The rasterizer
**must** be accessible via HTTP to the TileMill client.

In addition, references to MSS files, image resources, shapefile datasources,
and so on must all be available to the rasterizer via HTTP. While this is a
significant departure from many "typical" map designing workflows, it allows
TileMill projects to be portable between clients if set up properly.


Requirements
------------
- **TileMill client**: A modern standards compliant web browser. The developers
are currently testing with Chrome and Firefox 3.x.
- **TileMill server**: Apache/PHP 5.2+ or Python with the
[Tornado](http://www.tornadoweb.org/) web server.
- **Rasterizer**:
  - [TileLive](http://github.com/tmcw/TileLive)
  - [Mapnik 2.0](http://mapnik.org/)
  - [Cascadenik HEAD](http://mapnik-utils.googlecode.com/svn/trunk) from SVN

Setup
-----
### TileMill client

Put the `client` directory included with TileMill in a web-accessible directory
and open the URL to the directory in your web browser (e.g.
`http://localhost/TileMill/client` if you installed TileMill at your webroot).
If the TileMill client loads in your browser your installation was successful.

You may want to edit your `settings.js` file to adjust for your setup. In
particular, you can

- Choose a different server type. Currently only the `simple` HTTP based server
is supported.
- Set a different URL for your server. If your TileMill server will not be at
the standard location, `http://tilemill`, you can change this setting.
- Choose a different rasterizer type. Currently only the `tilelitelive`
rasterizer is supported.
- Set a different URL for your rasterizer. If your TileLiteLive server is not at
the standard location, `http://localhost:8888`, you can change this setting.

### TileMill server (Node.js)

Create directories called `project` and `visualization` in the TileLive
directory. Change to the `jsServer` directory and run `ndistro`. Then, run
`node tilemill.js` to start the server.

Authors
-------
- Dmitri Gaskin (dmitrig01)
- Young Hahn (yhahn)
- Tom MacWright (tmcw)
- AJ Ashton (ajashton)
