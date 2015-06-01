# heroku-buildpacks-sourceversion
Writes the SOURCE_VERSION variable (usually the Git SHA) to a file for use by the app.

Created by @sreid out of the need to show which Git commit version of an app was running on a Heroku instance. Made possible by the [addition of the SOURCE_VERSION variable during the build process](https://devcenter.heroku.com/changelog-items/630). This variable is available during the build process, but not available to a running app, making this approach neccessary. Suggestions and improvements appreciated!

## Usage
To use this buildpack, the app should already be successfully running the [multi buildpack](https://github.com/heroku/heroku-buildpack-multi).

Then just add this buildpack in addition to the existing buildpacks in the `.buildpacks` file:

	https://github.com/sreid/heroku-buildpack-sourceversion.git

In the application code, read the `.source_version` file that will be created on deployment. For example, in a Rails, it might look something like:

	git_sha = File.read(Rails.root.join('.source_version'))

(add any error handling for environments where this file doesn't exist, such as your development machine, of course...)

## License
MIT