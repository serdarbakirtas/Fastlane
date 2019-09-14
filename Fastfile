# This file contains the fastlane.tools configuration
# You can find the documentation at https://docs.fastlane.tools
#
# For a list of all available actions, check out
#
#     https://docs.fastlane.tools/actions
#
# For a list of all available plugins, check out
#
#     https://docs.fastlane.tools/plugins/available-plugins
#

# Uncomment the line if you want fastlane to automatically update itself
# update_fastlane

default_platform(:ios)

platform :ios do

	lane :unlock do |options|
	unlock_keychain(
	  path: options[:keychainPath],
	  password: options[:keychainPassword]
	)
	end

	lane :podinstall do 
	  cocoapods(repo_update: true, podfile: "./Podfile")
	end

	lane :example_sandbox_build do |options|
		path = gym(clean: true, configuration: "Debug.Staging", scheme: "ExampleProject", workspace: "ExampleProject.xcworkspace", export_method: "ad-hoc")
		params = { "path": path, "group": "ios-testers-beta", "user": options[:username], "api_token": options[:api_token], "app_name": options[:app_name] }
		upload params
	end

	lane :example_staging_build do |options|
		path = gym(clean: true, configuration: "Release.Internal.Staging", scheme: "ExampleProject", workspace: "ExampleProject.xcworkspace", export_method: "ad-hoc")
		params = { "path": path, "group": "ios-testers-staging", "user": options[:username], "api_token": options[:api_token], "app_name": options[:app_name] }
		upload params
	end

	lane :example_beta_build do |options|
		path = gym(clean: true, configuration: "Release.Internal.Production", scheme: "ExampleProject", workspace: "ExampleProject.xcworkspace", export_method: "ad-hoc")
		params = { "path": path, "group": "ios-testers-beta", "user": options[:username], "api_token": options[:api_token], "app_name": options[:app_name] }
		upload params
	end

	lane :example_release_build do
		path = gym(clean: true, configuration: "Release.Production", scheme: "ExampleProject", workspace: "ExampleProject.xcworkspace", export_method: "app-store")
	end

	lane :upload do |params|

		appcenter_upload(
  			api_token: params[:api_token],
  			owner_name: "example",
  			app_name: params[:app_name],
  			ipa: params[:path],
  			notify_testers: true
		)
  	end
end