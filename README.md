#!name=All In One + Spotify Lyric
#!desc=Full tính năng + đã fix lỗi + thêm lyric
#!author=duyvinh09 (mod by ChatGPT)
#!homepage=https://module-ios.netlify.app

[Rule]
AND,((DOMAIN-SUFFIX,googlevideo.com),(PROTOCOL,UDP)),REJECT
AND,((DOMAIN,youtubei.googleapis.com),(PROTOCOL,UDP)),REJECT

[Header Rewrite]
^https?://api.revenuecat.com/.+/(receipts$|subscribers/?(.?)$) header-del x-revenuecat-etag
^https?://api.revenuecat.com/.+/(receipts$|subscribers/?(.?)$) header-del X-RevenueCat-ETag

[Url Rewrite]
^https?://[\w-]+.googlevideo.com/(?!(dclk_video_ads|videoplayback?)).+&oad _ reject-200
^https?://(www|s).youtube.com/api/stats/ads _ reject-200
^https?://(www|s).youtube.com/(pagead|ptracking) _ reject-200
^https?://s.youtube.com/api/stats/qoe?adcontext _ reject-200
(^https?://[\w-]+.googlevideo.com/(?!dclk_video_ads).+?)&ctier=L(&.+?),ctier,(.+) $1$2$3 302

[Script]

YouTube Premium

youtube.request = type=http-request,pattern=^https://youtubei.googleapis.com/youtubei/v1/,requires-body=1,max-size=-1,binary-body-mode=1,script-path=https://raw.githubusercontent.com/duyvinh09/Module_IOS/main/js/youtube.response.js
youtube.response = type=http-response,pattern=^https://youtubei.googleapis.com/youtubei/v1/,requires-body=1,max-size=-1,binary-body-mode=1,script-path=https://raw.githubusercontent.com/duyvinh09/Module_IOS/main/js/youtube.response.js

Spotify Premium

spotify-json = type=http-request,pattern=^https://spclient.wg.spotify.com/,script-path=https://raw.githubusercontent.com/duyvinh09/Module_IOS/main/js/spotify-json.js
spotify-proto = type=http-response,pattern=^https://spclient.wg.spotify.com/,requires-body=1,binary-body-mode=1,script-path=https://raw.githubusercontent.com/duyvinh09/Module_IOS/main/js/spotify-proto.js

Spotify Lyric (🔥 thêm)

spotify-lyric = type=http-response,pattern=^https://spclient.wg.spotify.com/color-lyrics/v2/track/,requires-body=1,binary-body-mode=1,max-size=0,script-path=https://raw.githubusercontent.com/app2smile/rules/master/js/spotify-lyric.js,argument=appid=YOUR_APPID&securityKey=YOUR_KEY

SoundCloud

SoundCloudGo+ = type=http-response,pattern=https://api-mobile.soundcloud.com/configuration/ios,requires-body=1,script-path=https://raw.githubusercontent.com/duyvinh09/Module_IOS/main/js/SoundCloudGoPlus.js

AlightMotion

AlightMotion = type=http-response,pattern=^https://us-central1-alight-creative.cloudfunctions.net/getAccountStatusAndLicenses,requires-body=1,script-path=https://raw.githubusercontent.com/duyvinh09/Module_IOS/main/js/AlightMotion.js

PicsArt

PicsArt = type=http-request,pattern=^https://api.picsart.com/gw-v2/shop/subscription/apple/purchases,script-path=https://raw.githubusercontent.com/duyvinh09/Module_IOS/main/js/PicsArt.js

Wink

Wink = type=http-response,pattern=^https://api-sub.meitu.com/v2/user/vip_info_by_group.json,requires-body=1,script-path=https://raw.githubusercontent.com/duyvinh09/Module_IOS/main/js/WinkVipCrack.js

Truecaller

Truecaller = type=http-response,pattern=^https://premium-[^.]+.truecaller.com/,requires-body=1,script-path=https://raw.githubusercontent.com/duyvinh09/Module_IOS/main/js/TrueCaller.js

Kinemaster

Kinemaster = type=http-response,pattern=^https://api-account.kinemasters.com/,requires-body=1,script-path=https://raw.githubusercontent.com/duyvinh09/Module_IOS/main/js/Kinemaster.js

CamScanner

Camscanner = type=http-response,pattern=https://(api|api-cs.*).intsig.net/purchase/cs/query_property,requires-body=1,script-path=https://raw.githubusercontent.com/duyvinh09/Module_IOS/main/js/camScanner.js

BeautyPlus

BeautyPlus = type=http-response,pattern=https://(api.mr.pixocial.com|newbeee-api.beautyplus.com),requires-body=1,script-path=https://raw.githubusercontent.com/duyvinh09/Module_IOS/main/js/BeautyPlus.js

Locket (🔥 có rồi)

revenuecat = type=http-response,pattern=^https://api.revenuecat.com/,requires-body=1,script-path=https://raw.githubusercontent.com/duyvinh09/Module_IOS/main/js/Locket_DuyVinh09.js
deleteHeader = type=http-request,pattern=^https://api.revenuecat.com/,script-path=https://raw.githubusercontent.com/duyvinh09/Module_IOS/main/js/deleteHeader.js

[MITM]
hostname = %APPEND%, *.googlevideo.com, youtubei.googleapis.com, spclient.wg.spotify.com, api.revenuecat.com, api-mobile.soundcloud.com, api.picsart.com, api-sub.meitu.com, api-account.kinemasters.com, api.mr.pixocial.com, newbeee-api.beautyplus.com, *.intsig.net
