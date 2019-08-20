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

	lane :alnoor_sandbox_build do |options|
		path = gym(clean: true, configuration: "Debug.Staging", scheme: "ProjectName", workspace: "ProjectName.xcworkspace", export_method: "ad-hoc")
		params = { "path": path, "group": "ios-testers-beta", "user": options[:username] }
		upload params
	end

	lane :alnoor_staging_build do |options|
		path = gym(clean: true, configuration: "Release.Internal.Staging", scheme: "ProjectName", workspace: "ProjectName.xcworkspace", export_method: "ad-hoc")
		params = { "path": path, "group": "ios-testers-staging", "user": options[:username] }
		upload params
	end

	

	lane :alnoor_release_build do
		path = gym(clean: true, configuration: "Release.Production", scheme: "ProjectName", workspace: "ProjectName.xcworkspace", export_method: "app-store")
	end

	lane :upload do |params|

  		upload_to_testflight(
		  beta_app_feedback_email: "serdar.bakirtas@alnoortv.com",
		  demo_account_required: false,
		  notify_external_testers: false,
		  app_identifier: params[:app_id],
		  ipa: params[:path],
		  skip_submission: true,
		  username: params[:user]
		)
  	end
end

