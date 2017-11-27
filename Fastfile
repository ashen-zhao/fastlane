# Customize this file, documentation can be found here:
# https://docs.fastlane.tools/actions/
# All available actions: https://docs.fastlane.tools/actions
# can also be listed using the `fastlane actions` command

# Change the syntax highlighting to Ruby
# All lines starting with a # are ignored when running `fastlane`

# If you want to automatically update fastlane if a new version is available:
# update_fastlane

# This is the minimum version number required.
# Update this, if you use features of a newer version
fastlane_version "2.66.0"

default_platform :ios



platform :ios do
  @BUILD_NUM = ""
  before_all do
    ENV["SLACK_URL"] = "https://hooks.slack.com/services/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"
    # cocoapods
    # carthage
  end

  desc "Runs all the tests"
  lane :test do
    scan
  end


  ##########################################################################
  lane :sethost do|options|
    hosturl = options[:hosturl]
    hosturlapp = options[:hosturlapp]
    hosturlnewapp = options[:hosturlnewapp]
    hosturlshop = options[:hosturlshop]
    hostplist = "./ULife/Libraries/LibSuperReal/Resource.bundle/Resources/Config.plist"
    set_info_plist_value(path: hostplist, key: "hostURL",value:hosturl)
    set_info_plist_value(path: hostplist, key: "hostURLAPP",value:hosturlapp)
    set_info_plist_value(path: hostplist, key: "hostURLNEWAPP",value:hosturlnewapp)
    set_info_plist_value(path: hostplist, key: "hostURLSHOP",value:hosturlshop)
  end

  lane :testhost do
    sethost(hosturl:"http://118.31.213.38", hosturlapp:"http://118.31.211.209", hosturlnewapp:"http://101.37.135.172", hosturlshop:"http://118.31.211.208")
  end
  lane :devhost do
    sethost(hosturl:"http://192.168.1.9:8800", hosturlapp:"http://192.168.1.9:8800", hosturlnewapp:"http://192.168.1.9:8070", hosturlshop:"http://192.168.1.9:8800")
  end
  lane :releasehost do
    sethost(hosturl:"", hosturlapp:"", hosturlnewapp:"https://loan.uubee.com", hosturlshop:"https://small.uubee.com")
  end


  lane :build do|options|

    method = options[:method]

    currentTime = Time.new.strftime("%y%m%d")
    buildno = get_build_number()
    BUILD_NUM = buildno
    if buildno.include?"#{currentTime}"
       # => 为当天版本 计算迭代版本号
      lastStr = build[buildno.length-2..buildno.length-1]
      lastNum = lastStr.to_i
      lastNum = lastNum + 1
      lastStr = lastNum.to_s
      if lastNum < 10
        lastStr = lastStr.insert(0,"0")
      end
      buildno = "#{currentTime}#{lastStr}"
    else
      buildno = "#{currentTime}01"
    end

    increment_build_number_in_plist(target: ENV['SCHEME_NAME'], build_number: buildno)
    increment_version_number_in_plist(target: ENV['SCHEME_NAME'], version_number: ENV['APP_VERSION'])


    outputDir = "./fastlane/build/#{Time.now.strftime('%y%m%d')}"
    outputName = "#{ENV['SCHEME_NAME']}-#{Time.now.strftime("%Y-%m-%d %H:%M:%S")}"

    # 创建生成证书
    # cert(output_path: outputDir + "/#{ENV['SCHEME_NAME']}/cert")
    # 创建描述文件pp
    # sigh(output_path: outputDir + "/#{ENV['SCHEME_NAME']}/sign")

    gym(
      clean: true,  # 在构建前先clean
      silent: true,  # 隐藏没有必要的信息
      scheme: ENV['SCHEME_NAME'],
      configuration: "Release",
      export_method:method,
      output_directory: outputDir,
      output_name: outputName,
      include_bitcode: false
    )
  end

  desc "上传到蒲公英"
  lane :to_pgyer do|options|
    build(method:"ad-hoc")
    txt = options[:txt]
    pgyer(api_key: "81b2cc1f257067babe9bfbdb4de90031", user_key: "7ae62d3b148cab7ec32459d9ecd657bc", update_description: txt)    
  end
  desc "开发环境上传到蒲公英"
  lane :to_pgyer_dev do|options|
    testhost
    txt = options[:txt]
    to_pgyer(txt:txt)
  end
  desc "测试环境上传到蒲公英"
  lane :to_pgyer_test do|options|
    testhost
    txt = options[:txt]
    to_pgyer(txt:txt)
  end
  desc "线上环境上传到蒲公英"
  lane :to_pgyer_release do|options|
    testhost
    txt = options[:txt]
    to_pgyer(txt:txt)
  end
  

  desc "上传到iTC"
  lane :to_appstore do 
    releasehost
    build(method:"app-store")
    pilot(skip_waiting_for_build_processing:true)
  end

  after_all do |lane|
    slack(
      message: "Successfully deployed new App Update."
    )
  end

  error do |lane, exception|
    increment_build_number_in_plist(target: ENV['SCHEME_NAME'], build_number: BUILD_NUM)
    slack(
      message: exception.message,
      success: false
    )
  end
end


# More information about multiple platforms in fastlane: https://docs.fastlane.tools/advanced/#control-configuration-by-lane-and-by-platform
# All available actions: https://docs.fastlane.tools/actions

# fastlane reports which actions are used. No personal data is recorded.
# Learn more at https://docs.fastlane.tools/#metrics
