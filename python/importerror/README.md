1. Run buildout to set up your app


	```
	$ python bootstrap.py
	$ ./bin/buildout
	```

2. Launch app using generated dev_appserver script

	```
    ./bin/dev_appserver
    ```

3. Logs will show error about importing `google.appengine.dist27.threading`

4. Open `app.yaml` and comment out [line 41](https://github.com/Trii/appengine-examples/blob/53e9f94a2ff108e41d34978c941d8bacaa49d29e/python/importerror/app.yaml#L41)

5. Relaunch the app and the error goes away

The buildout recipe `appfy.recipe.gae` downloads the latest SDK and umpacks it into buildout's `parts` directory. It seems that at some point in time, the `dev_appserver` sandbox ignores items listed in skip_files which prevents the import. This is strange though because other items are imported correctly.

*Commenting / Uncommenting the line in `app.yaml` is enough to trigger the behavior*
