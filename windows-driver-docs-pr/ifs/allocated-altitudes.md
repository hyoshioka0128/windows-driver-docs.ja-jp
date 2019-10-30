---
title: 割り当て済み高度
description: 割り当て済み高度
ms.assetid: EC1993FB-5219-4C0C-A76A-05937A461C5A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 703112d39982e4a4fef84d62fbcbed2f38a16131
ms.sourcegitcommit: 5e257e7d54d77649b4981a55a7d61676a3b25f00
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73064151"
---
# <a name="allocated-altitudes"></a>割り当て済み高度

フィルターマネージャーモデルに対して開発されたファイルシステムミニパスのドライバーは、ファイルシステムスタック内に存在する他のミニフィルターとの相対的な位置を定義する高度と呼ばれる一意の識別子を持っている必要があります。 ミニフィルターの高度は、ミニフィルターの要件と負荷の順序のグループに基づいて Microsoft によって割り当てられます。

ミニフィルターの高度な数値を要求するには、「[ミニフィルターの高度な要求](minifilter-altitude-request.md)」を参照してください。

現在の標高割り当ては、次の各読み込み順序グループについて以下に示します。

## <a name="span-id420000_-_429999__filterspanspan-id420000_-_429999__filterspanspan-id420000_-_429999__filterspan420000---429999-filter"></a><span id="420000_-_429999__Filter"></span><span id="420000_-_429999__filter"></span><span id="420000_-_429999__FILTER"></span>42万-429999: フィルター

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| ntoskrnl.exe | 425500 | [Microsoft] |
| ntoskrnl.exe | 425000 | [Microsoft] |

## <a name="span-id400000_-_409999__fsfilter_topspanspan-id400000_-_409999__fsfilter_topspanspan-id400000_-_409999__fsfilter_topspan400000---409999-fsfilter-top"></a><span id="400000_-_409999__FSFilter_Top"></span><span id="400000_-_409999__fsfilter_top"></span><span id="400000_-_409999__FSFILTER_TOP"></span>40万-409999: FSFilter Top

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| wcnfs .sys | 409900 | [Microsoft] |
| bindflt | 409800 | [Microsoft] |
| cldflt | 409500 | [Microsoft] |
| iorate | 409010 | [Microsoft] |
| ioqos .sys | 409000 | [Microsoft] |
| fsdepends .sys に依存します | 407000 | [Microsoft] |
| sftredir | 406000 | [Microsoft] |
| dfs-r | 405000 | [Microsoft] |
| tracker | 404910 | Acronis |
| csvnsflt | 404900 | [Microsoft] |
| csvflt | 404800 | [Microsoft] |
| Uev. AgentDriver. .sys | 404710 | [Microsoft] |
| AppvVfs | 404700 | [Microsoft] |
| CCFFilter .sys | 404600 | [Microsoft] |
| dciogrd | 402010 | Datacloak Tech |
| Dewdrv .sys | 402000 | Dell テクノロジ |
| zsusbstorfilt | 401910 | Zshield Inc. |
| eaw .sys | 401900 | Raytheon サイバーソリューション |
| TVFsfilter | 401800 | TrustView |
| KKDiskProtecter | 401700 | Goldmsg |
| AgentComm | 401600 | Trustwave 持株 Inc. |
| rvsavd | 401500 | CJSC Returnil ソフトウェア |
| DGMinFlt | 401410 | デジタルガーディアン Inc. |
| dgdmk | 401400 | Verdasys Inc. |
| tusbstorfilt | 401300 | SimplyCore の場合 |
| pcgenfam .sys | 401200 | Soluto |
| atrsdfw .sys | 401100 | Altiris |
| tpfilter .sys | 401000 | RedPhone のセキュリティ |
| MBIG2Prot | 400920 | Malwarebytes Inc. |
| mbamwatchdog .sys | 400900 | Malwarebytes Corporation |
| DSESafeCtrlDrv | 400803 | 上海 Eff-ソフト IT |
| edevmon | 400800 | ESET spol。 s r.o. |
| vmwflstor .sys | 400700 | VMware, Inc. |
| TsQBDrv .sys | 400600 | Tencent テクノロジ |
| WRAEKernel | 400500 | Webroot Inc. |

## <a name="span-id360000_-_389999__fsfilter_activity_monitorspanspan-id360000_-_389999__fsfilter_activity_monitorspanspan-id360000_-_389999__fsfilter_activity_monitorspan360000---389999-fsfilter-activity-monitor"></a><span id="360000_-_389999__FSFilter_Activity_Monitor"></span><span id="360000_-_389999__fsfilter_activity_monitor"></span><span id="360000_-_389999__FSFILTER_ACTIVITY_MONITOR"></span>36万-389999: FSFilter 利用状況モニター

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| klboot | 389510 | Kaspersky ラボ |
| klfdefsf | 389500 | Kaspersky ラボ |
| CBFSFilter2017 | 389250 | SecureLink Inc. |
| NWEDriver .sys | 389240 | Dell テクノロジ |
| cytmon. sys | 389230 | Cytrence Inc. |
| SophosED | 389220 | Sophos |
| .Sys | 389210 | Somma Inc. |
| IFS64 | 389200 | Ashampoo 開発 |
| TSTFilter | 389190 | ThinScale Tech |
| VrnsFilter .sys | 389180 | Varonis Ltd. |
| lrtp. sys | 389170 | Lenovo 北京 |
| ipcomfltr | 389160 | Bluzen Inc. |
| SvCBT | 389150 | Spハーソフトテクノロジ |
| mbamshuriken. sys | 389140 | Malwarebytes |
| ContainerMonitor | 389130 | 水色のセキュリティ |
| SaMFlt | 389120 | DreamCrafts |
| RuiMinispy | 389117 | このように |
| RuiFileAccess | 389115 | このように |
| システムの | 389113 | このように |
| . Sys | 389111 | このように |
| windd .sys | 389110 | Comae 技術 |
| cbfsfilter2017 | 389105 | ネットワークでの base |
| taobserveflt | 389100 | ThinAir Labs Inc. |
| vollock .sys | 389092 | Man テクノロジ Inc. |
| drbdlock | 389090 | Man テクノロジ Inc. |
| dcfsgrd | 389085 | Datacloak Tech |
| hsmltmon | 389080 | Hitachi ソリューション |
| AternityRegistryHook | 389070 | Aternity Ltd. |
| MozyNextFilter | 389068 | Carbonite Inc. |
| MozyCorpFilter | 389067 | Carbonite Inc. |
| MozyEntFilter | 389066 | Carbonite Inc. |
| MozyOEMFilter | 389065 | Carbonite Inc. |
| MozyEnterpriseFilter | 389064 | Carbonite Inc. |
| MozyProFilter | 389063 | Carbonite Inc. |
| MozyHomeFilter | 389062 | Carbonite Inc. |
| BDSFilter .sys | 389061 | Carbonite Inc. |
| CSBFilter .sys | 389060 | Carbonite Inc. |
| ChemometecFilter | 389050 | ChemoMetec |
| SentinelMonitor | 389040 | SentinelOne |
| DhWatchdog | 389030 | [Microsoft] |
| edrsensor .sys | 389025 | Bitdefender SRL |
| bdprivmon | 389022 | Bitdefender SRL |
| NpEtw. sys | 389020 | お金 |
| OczMiniFilter フィルター sys | 389010 | OCZ ストレージ |
| ielcp | 389004 | Intel Corporation |
| IESlp | 389002 | Intel Corporation |
| IntelCAS | 389000 | Intel Corporation |
| boxifier | 388990 | Kenubi |
| SamsungRapidFSFltr | 388980 | NVELO Inc. |
| drsfile | 388970 | MRY います。 |
| CbFltFs4 | 388966 | Simopro テクノロジ |
| CrUnCopy | 388964 | Shenzhen CloudRiver |
| aictracedrv_am | 388960 | AI コンサルティング |
| fiopolicyfilter | 388954 | SanDisk Inc. |
| fcontrol .sys | 388950 | SODATSW spol。 s r.o. |
| qfilter .sys | 388940 | クォーラムラボ |
| Redlight .sys | 388930 | Trustware Ltd. |
| .eps | 388920 | Lumension |
| VHDTrack | 388915 | 会社 onis Inc. |
| VHDDelta | 388912 | Niriva の場合 |
| FSTrace | 388910 | Niriva の場合 |
| YahooStorage | 388900 | Yahoo 日本 Corporation |
| KeWF .sys | 388890 | KEBA AG |
| epregflt | 388888 | チェックポイントソフトウェア |
| epklib .sys | 388886 | チェックポイントソフトウェア |
| zsfprt | 388880 | k4solution Co。 |
| dsflt | 388876 | cEncrypt |
| bfaccess .sys | 388872 | bitFence Inc. |
| xcpl. sys | 388870 | X-クラウドシステム |
| DCFAFilter .sys | 388866 | ManageEngine Zoho |
| RMPHVMonitor .sys | 388865 | ManageEngine Zoho |
| FAPMonitor .sys | 388864 | ManageEngine Zoho |
| EaseFlt | 388860 | EaseVault テクノロジ Inc. |
| rpq ウォッチャー | 388855 | 最高のセキュリティ |
| sieflt | 388852 | 迅速な回復テクノロジ Pvt。 社. |
| cssdlp | 388851 | 迅速な回復テクノロジ Pvt。 社. |
| cssdlp | 388850 | CoSoSys |
| INISBDrv64 | 388840 | Initech Inc. |
| トレース .sys | 388831 | Fitsec Ltd. |
| SandDriver | 388830 | Fitsec Ltd. |
| dskmn | 388820 | Honeycomb テクノロジ |
| xkfsfd .sys | 388810 | Jiransoft Co、Ltd. |
| pcpifd .sys | 388800 | Jiransoft Co、Ltd. |
| NNTInfo .sys | 388790 | 新しいネットテクノロジが制限されています |
| FsMonitor .sys | 388780 | IBM |
| CVCBT .sys | 388770 | CommVault Systems, Inc. |
| AwareCore | 388760 | TaaSera Inc. |
| laFS. sys | 388750 | NetworkProfi Ltd. |
| fsnk | 388740 | SoftPerfect な研究 |
| RGNT .sys | 388730 | HFN Inc. |
| fltRs329 | 388720 | セキュリティで保護された地球 Inc. |
| ospmon | 388710 | SC ODEKIN SOLUTIONS の SRL |
| edsigk .sys | 388700 | Enterprise Data Solutions, Inc. |
| fiometer | 388692 | Fusion-io |
| dcSnapRestore .sys | 388690 | Fusion-io |
| fam. sys | 388680 | 迅速な回復テクノロジ Pvt。 社. |
| vidderfs | 388675 | Vidder Inc. |
| Tritiumfltr | 388670 | Tritium Inc. |
| HexisFSMonitor | 388660 | Hexis サイバーソリューション |
| BlackbirdFSA | 388650 | BeyondTrust Inc. |
| TMUMS | 388642 | Trend Micro Inc. |
| hfileflt | 388640 | Trend Micro Inc. |
| TMUMH .sys | 388630 | Trend Micro Inc. |
| AcDriver .sys | 388620 | Trend Micro, Inc. |
| SakFile | 388610 | Trend Micro, Inc. |
| SakMFile | 388600 | Trend Micro, Inc. |
| rsfdrv .sys | 388580 | Clonix Co |
| alcapture. sys | 388570 | エアロックデジタル Pty Ltd. |
| kmNWCH | 388560 | IGLOO SOFTWARE SECURITY, Inc. |
| ISIRMFmon | 388550 | アルプスのシステム統合 CO。 |
| EsProbe. sys | 388542 | Stormshield |
| heimdall | 388540 | Arkoon のネットワークセキュリティ |
| thetta | 388532 | Syncopate |
| thetta | 388531 | Syncopate |
| thetta | 388530 | Syncopate |
| DTPL. sys | 388520 | CONNECT SHIFT LTD. |
| CyOptics .sys | 388514 | Cylance Inc. |
| CyProtectDrv32 | 388510 | Cylance Inc. |
| CyProtectDrv64 | 388510 | Cylance Inc. |
| tbfsfilt | 388500 | 3番目のやバケツリレー |
| IvAppMon | 388491 | Ivanti |
| LDSecDrv .sys | 388490 | LANDESK ソフトウェア |
| SGResFlt | 388480 | Samsung SDS Ltd. |
| CwMem2k64 | 388470 | ApSoft |
| axfltdrv .sys | 388460 | Axact Pvt Ltd. |
| RMDiskMon .sys | 388450 | Qingdao の Anmei ネットワークテクノロジ Co。 |
| diskactmon .sys | 388440 | Qingdao の Anmei ネットワークテクノロジ Co。 |
| Codex .sys | 388430 | いいね。 |
| CatMF .sys | 388420 | Logichron Inc. |
| RW7FsFlt | 388410 | PJSC KP VTI |
| aswSP. sys | 388401 | Avast ソフトウェア |
| aswFsBlk. sys | 388400 | ALWIL ソフトウェア |
| ThreatStackFIM | 388380 | 脅威スタック |
| BOsCmFlt | 388370 | Barkly は Inc. を保護します。 |
| BOsFsFltr | 388370 | Barkly は Inc. を保護します。 |
| FeKern。 sys | 388360 | 焼討 |
| libwamf | 388350 | OPSWAT Inc. |
| SZEDRDrv .sys | 388346 | 安全です。 |
| szシャード | 388345 | 安全です。 |
| szpcmdrv | 388341 | 安全です。 |
| szdfmdrv .sys | 388340 | 安全です。 |
| szdfmdrv_usb | 388331 | 安全です。 |
| sprtdrv | 388330 | 安全です。 |
| SWFsFltrv2 | 388321 | お金 |
| SWFsFltr | 388320 | お金 |
| flashaccelfs | 388310 | ネットワークアプライアンス |
| changelog | 388300 | ネットワークアプライアンス |
| stcvsm .sys | 388250 | StorageCraft Tech |
| システム | 388240 | ITSTATION Inc. |
| fshs | 388222 | F-セキュリティ保護 |
| fshs | 388221 | F-セキュリティ保護 |
| fsatp .sys | 388220 | F-セキュリティ保護 |
| SecdoDriver .sys | 388210 | Secdo |
| TGFSMF | 388200 | Tetraglyph テクノロジ |
| evscase .sys | 388100 | 3月の h Software Ltd. |
| VSScanner. sys | 388050 | VoodooSoft |
| HDRansomOffDrv | 388044 | He・ g の防御 |
| HDCorrelateFDrv | 388042 | He・ g の防御 |
| HDFileMon. sys | 388040 | He・ g の防御 |
| tsifilemon. sys | 388012 | インターコム Inc. |
| MarSpy. sys | 388010 | インターコム Inc. |
| AGSysLock .sys | 388002 | AppGuard の場合 |
| AGSecLock .sys | 388001 | AppGuard の場合 |
| BrnFileLock .sys | 388000 | Blue ねじ山 Networks |
| BrnSecLock .sys | 387990 | Blue ねじ山 Networks |
| LCmPrintMon | 387978 | YATEM Co. Ltd. |
| LCgAdMon | 387977 | YATEM Co. Ltd. |
| LCmAdMon | 387976 | YATEM Co. Ltd. |
| LCgFileMon .sys | 387975 | YATEM Co. Ltd. |
| LCmFile | 387974 | YATEM Co. Ltd. |
| LCgFile .sys | 387972 | YATEM Co. Ltd. |
| LCmFileMon | 387970 | YATEM Co. Ltd. |
| IridiumSwitch | 387960 | # O |
| scensemon | 387950 | AppiXoft |
| ruaff | 387940 | RUNEXY |
| bbfilter .sys | 387930 | derivo GmbH |
| Bfmon | 387920 | Baidu (香港) 限定 |
| bdsysmon | 387912 | Baidu Online ネットワーク |
| BdRdFolder .sys | 387910 | Baidu (北京) |
| ml、.sys | 387901 | RUNEXY |
| pscff .sys | 387900 | Weing、Ltd.、 |
| fcnotify .sys | 387880 | TCXA Ltd. |
| aaf. sys | 387860 | Actifio Inc. |
| gddcv | 387840 | G データソフトウェア AG |
| wgfile | 387820 | オレンジ色の WERKS Inc. |
| zesfsmf .sys | 387800 | 社 |
| uamflt | 387700 | Sevtechnotrans |
| ehdrv .sys | 387600 | ESET、spol。 s r.o. |
| DattoFSF | 387560 | Datto Inc. |
| FileSystemCBT | 387550 | Rubrik Inc. |
| Snilog .sys | 387500 | Systemneeds 必要性, Inc. |
| tss | 387400 | Tiversa Inc |
| LmDriver .sys | 387390 | ソフト Kft。 |
| WDCFilter .sys | 387330 | Interset Inc. |
| altcbt .sys | 387320 | Altaro Ltd. |
| bapfecpt | 387310 | BitArmor システム、Inc. |
| bamfltr | 387300 | BitArmor システム、Inc. |
| TrustedEdgeFfd .sys | 387200 | FileTek, Inc. |
| MRxGoogle | 387100 | Google, Inc. |
| YFSDR。SYS.DATABASES | 387010 | Yokogawa R & L Corp |
| YFSD.SYS.DATABASES | 387000 | Yokogawa R & L Corp |
| YFSRD sys | 386990 | Yokogawa R & L Corp |
| psgfoctrl | 386990 | Yokogawa R & L Corp |
| psgdflt | 386980 | Yokogawa R & L Corp |
| USBPDH。SYS.DATABASES | 386901 | 高度なコンピューティングを開発するためのセンター |
| pecfilter | 386900 | C-DAC ハイデラバード |
| G/FCB. sys | 386810 | インカインターネット Co。 |
| GKPFCB64 | 386810 | インカインターネット Co。 |
| 32ビットの TkPcFtCb | 386800 | インカインターネット Co., Ltd. |
| TkPcFtCb64 (64 ビット) | 386800 | インカインターネット Co., Ltd. |
| bmregdrv .sys | 386731 | Yandex の場合 |
| bmfsdrv .sys | 386730 | Yandex の場合 |
| CarbonBlackK | 386720 | Bit9 Inc. |
| ScAuthFSFlt | 386710 | セキュリティコードの例 |
| ScAuthIoDrv .sys | 386700 | セキュリティコードの例 |
| mfeaskm | 386610 | McAfee Inc. |
| mfencfilter .sys | 386600 | McAfee |
| WinFLAHdrv | 386540 | NewSoftwares&#x2024;Net, inc. |
| WinFLAdrv. sys | 386530 | NewSoftwares&#x2024;Net, inc. |
| WinDBdrv .sys | 386520 | NewSoftwares&#x2024;Net, inc. |
| WinFLdrv .sys | 386510 | NewSoftwares&#x2024;Net, inc. |
| WinFPdrv. sys | 386500 | NewSoftwares&#x2024;Net, inc. |
| SkyWPDrv | 386435 | スカイ Co., Ltd. |
| SkyRGDrv | 386431 | スカイ Co., LTD. |
| SkyAMDrv | 386430 | スカイ Co., LTD. |
| SheedSelfProtection. sys | 386421 | SheedSoft Ltd. |
| arta | 386420 | SheedSoft Ltd. |
| ApexSqlFilterDriver .sys | 386410 | ApexSQL の場合 |
| stflt | 386400 | Xacti |
| tbrdrv .sys | 386390 | クローラーグループ |
| WinTeonMiniFilter フィルター | 386320 | Dmitry Stefankov |
| ワイパー | 386310 | Dmitry Stefankov |
| DevMonMiniFilter システム | 386300 | Dmitry Stefankov |
| VMWVvpfsd | 386200 | VMware, Inc. |
| RTOLogon (名前の変更) | 386200 | VMware, Inc. |
| Code42Filter | 386190 | Code42 |
| ConduantFSFltr | 386180 | Conduant Corporation |
| KtFSFilter .sys | 386170 | 鍵視テクノロジ |
| FileGuard. sys | 386140 | RES ソフトウェア |
| NetGuard. sys | 386130 | RES ソフトウェア |
| RegGuard. sys | 386120 | RES ソフトウェア |
| ImgGuard | 386110 | RES ソフトウェア |
| AppGuard. sys | 386100 | RES ソフトウェア |
| 自分の Idiskfs .sys | 386030 | このように |
| minitrc | 386020 | 保護されたネットワーク |
| cpepmon | 386010 | チェックポイントソフトウェア |
| CGWMF. sys | 386000 | NetIQ |
| ISRegFlt | 385990 | Flexera Software Inc. |
| ISRegFlt64 | 385990 | Flexera Software Inc. |
| shdlpSf | 385970 | Comtrue テクノロジ |
| ctrPAMon | 385960 | Comtrue テクノロジ |
| shdlpMedia .sys | 385950 | Comtrue テクノロジ |
| immflex | 385910 | Immidio B.V. |
| StegoProtect | 385900 | Stegosystems Inc. |
| brfilter .sys | 385890 | Bromium Inc. |
| BrCow_x_x_x_x | 385889 | Bromium Inc. |
| BemK | 385888 | Bromium Inc. |
| secRMM .sys | 385880 | Squadra テクノロジ |
| dgfilter | 385870 | DataGravity Inc. |
| WFP_MRT | 385860 | 焼討アイ Inc. |
| klrsps | 385815 | Kaspersky ラボ |
| klsnsr | 385810 | Kaspersky ラボ |
| TaniumRecorderDrv | 385800 | Tanium |
| mssecflt | 385600 | [Microsoft] |
| Backupreader | 385500 | [Microsoft] |
| MsixPackagingToolMonitor | 385410 | [Microsoft] |
| AppVMon | 385400 | [Microsoft] |
| DpmFilter .sys | 385300 | [Microsoft] |
| Procmon11 | 385200 | [Microsoft] |
| minispy-Top | 385100 | [Microsoft] |
| fdrtrace | 385001 | [Microsoft] |
| filetrace .sys | 385000 | [Microsoft] |
| uwfreg .sys | 384910 | [Microsoft] |
| uwfs .sys | 384900 | [Microsoft] |
| locksmith. sys | 384800 | [Microsoft] |
| winload .sys | 384700 | [Microsoft] |
| SFPMonitor .sys-Top | 383350 | SonicWall Inc. |
| FilrDriver .sys | 383340 | マイクロフォーカス |
| rwの場合 | 383330 | Rackware |
| airship-filter | 383320 | エアウェアテクノロジ Ltd. |
| AeFilter | 383310 | Faronics Corporation |
| QQProtect. sys | 383300 | Tencent (Shenzhen) |
| QQProtectX64 | 383300 | Tencent (Shenzhen) |
| KernelAgent32 | 383260 | ゾーン |
| WRDWIZFILEPROT.SYS.DATABASES | 383251 | WardWiz |
| WRDWIZREGPROT.SYS.DATABASES | 383250 | WardWiz |
| groundling32 | 383200 | Dell Secureworks |
| groundling64 | 383200 | Dell Secureworks |
| avgtpx86 | 383190 | 平均テクノロジ CS-CZ |
| avgtpx64 | 383190 | 平均テクノロジ CS-CZ |
| DataNow_Driver | 383182 | AppSense Ltd. |
| UcaFltDriver | 383180 | AppSense Ltd. |
| YFSD2 | 383170 | Yokogawa Corpration |
| Kisknl | 383160 | 王国 |
| MWatcher. sys | 383150 | Neowiz Corporation |
| tsifilemon. sys | 383140 | インターコム Inc. |
| FIM. sys | 383130 | eIQnetworks Inc. |
| cFSfdrv | 383120 | Chaewool |
| ajfsprot | 383110 | 分析 tik Jena AG |
| isafermon | 383100 | 40u-cSMS |
| kfac | 383000 | 北京 CA-JinChen ソフトウェア Co。 |
| GUMHFilter .sys | 382910 | Glarysoft Ltd. |
| PsAcFileAccessFilter .sys | 382902 | 富士通のソフトウェア |
| FJGSDis2 | 382900 | 富士通限定 |
| secure_os | 382890 | 富士通のソーシャルサイエンス |
| ibr2fsk | 382880 | 富士通工学 |
| FJSeparettiFilterRedirect | 382860 | 富士通限定 |
| Fsw31rj1 | 382855 | 富士通限定 |
| da_ctl | 382850 | 富士通限定 |
| zqFilter .sys | 382800 | magrasoft Ltd. |
| ntps_fa | 382700 | NTP ソフトウェア |
| sConnect .sys | 382600 | I/O データデバイス |
| AdaptivaClientCache32 | 382500 | Adaptiva |
| AdaptivaclientCache64 | 382500 | Adaptiva |
| phantomd | 382440 | Veramine Inc. |
| GoFSMF .sys | 382430 | Gorizonty Rosta Ltd. |
| SWCommFltr | 382420 | SnoopWall の場合 |
| atflt | 382410 | Atlansys ソフトウェア |
| amfd .sys | 382400 | Atlansys ソフトウェア |
| iSafeKrnl | 382390 | Elex Tech Inc. |
| iSafeKrnlMon | 382380 | Elex Tech Inc. |
| Qutmdrv .sys | 382320 | 360ソフトウェア (北京) |
| 360box | 382310 | Qihoo 360 |
| 360fsflt | 382300 | 北京 Qihoo テクノロジ Co。 |
| scred | 382210 | ソフトキャンプ Co。 |
| PDGenFam .sys | 382200 | Soluto LTD. |
| MCFileMon64 (x64 システム) | 382100 | Sumitomo 電気 |
| MCFileMon32 (x32 systems) | 382100 | Sumitomo 電気 |
| RyGuard | 382050 | SHENZHEN UNNOO Information のテクニカル Co。 |
| FileShareMon | 382040 | SHENZHEN UNNOO Information のテクニカル Co。 |
| ryfilter | 382030 | SHENZHEN UNNOO Information のテクニカル Co。 |
| secufile | 382020 | Shenzhen Unnoo LTD. |
| XiaobaiFs | 382010 | Shenzhen Unnoo LTD. |
| XiaobaiFsR | 382000 | Shenzhen Unnoo LTD. |
| TWBDCFilter | 381910 | Trustwave |
| VPDrvNt | 381900 | AhnLab, Inc. |
| eetd32 | 381800 | Entrust Inc. |
| eetd64 | 381800 | Entrust Inc. |
| dnaFSMonitor .sys | 381700 | Dtex システム |
| 2000の iwhlp2 | 381610 | InfoWatch |
| XP の iwhlpxp | 381610 | InfoWatch |
| Vista の iwhlp | 381610 | InfoWatch |
| iwdmfs | 381600 | InfoWatch |
| IronGateFD | 381500 | rubysoft |
| MagicBackupMonitor | 381400 | マジック Softworks, Inc. |
| Sonar .sys | 381337 | IKARUS のセキュリティ |
| IPFilter | 381310 | Jinfengshuntai |
| MSpy | 381300 | Ladislav Zezula |
| . sys | 381200 | 3月の h Software Ltd. |
| qfmon | 381190 | 品質 Corporation |
| flyfs | 381160 | NEC ソフト |
| serfs | 381150 | NEC ソフト |
| hdrfs | 381140 | NEC ソフト |
| UVMCIFSF | 381130 | NEC Corporation |
| ICFClientFlt | 381120 | NEC システムテクノロジ、Ltd. |
| IccFileIoAd | 381110 | NEC システムテクノロジ、Ltd. |
| IccFilterAudit. sys | 381100 | NEC システムテクノロジ |
| IccFilterSc | 381090 | InfoCage |
| Sefo. sys-Top | 381010 | お金 |
| mtsvcdf .sys | 381000 | 境界 |
| SQLsafeFilterDriver .sys | 380901 | Idera ソフトウェア |
| IderaFilterDriver .sys | 380900 | Idera |
| cbfsfilter2017 | 380850 | SN Systems Ltd. |
| xhunter1 | 380800 | Wellbia&#x2024;com |
| iGuard | 380720 | i-ガード SAS |
| cbfltfs4 | 380715 | Nomadesk |
| cbfltfs4 | 380710 | バックアップシステム Ltd. |
| PkgFilter .sys | 380700 | スケーラブルなソフトウェア Inc. |
| snimg. sys | 380600 | Softnext テクノロジ |
| SK | 380520 | ヒートソフトウェア |
| mpxmon | 380510 | 肯定的テクノロジ |
| filenamevalidator | 380502 | Infotecs |
| KC3 | 380500 | Infotecs |
| PLPOffDrv .sys | 380492 | SK Infosec 共同 |
| ISFPDrv .sys | 380491 | SK Infosec 共同 |
| ionmonwdrv | 380490 | SK Infosec 共同 |
| Sefo .sys-中間 | 380480 | お金 |
| sagntflt | 380470 | ShinNihonSystec Co |
| VrExpDrv | 380460 | Hauri Inc. |
| srminifilterdrv .sys | 380450 | Citrix システム |
| zzpensys | 380440 | Jshan Jing an |
| tedrdrv .sys | 380430 | Palo Alto Networks |
| fangcloud_autolock_driver | 380420 | Hangzhou Yifangyun |
| CbSampleDrv .sys | 380020 | [Microsoft] |
| CbSampleDrv .sys | 380010 | [Microsoft] |
| CbSampleDrv .sys | 38万 | [Microsoft] |
| 簡略化した担当者 | 371100 | [Microsoft] |
| 変更、.sys | 370160 | [Microsoft] |
| delete_flt | 370150 | [Microsoft] |
| SmbResilFilter | 370140 | [Microsoft] |
| usbtest | 370130 | [Microsoft] |
| NameChanger | 370120 | [Microsoft] |
| failMount .sys | 370110 | [Microsoft] |
| failAttach .sys | 370100 | [Microsoft] |
| stest | 370090 | [Microsoft] |
| cdo .sys | 370080 | [Microsoft] |
| ctx | 370070 | [Microsoft] |
| fmm .sys | 370060 | [Microsoft] |
| cancelSafe | 370050 | [Microsoft] |
| メッセージ .sys | 370040 | [Microsoft] |
| パススルー | 370030 | [Microsoft] |
| nullFilter .sys | 370020 | [Microsoft] |
| ntest. sys | 370010 | [Microsoft] |
| minispy-中間 | 37万 | [Microsoft] |
| isecureflt | 368530 | iSecure Ltd. |
| SFPMonitor .sys-中央 | 368520 | SonicWall Inc. |
| wats_se | 368510 | Fujian Shen |
| secure_os_mf | 368500 | HAURI |
| FileMonitor | 368470 | Cygna Labs |
| asiofms .sys | 368460 | テクノロジを奨励する |
| cbfsfilter2017 | 368450 | 絶対ソフトウェア |
| FileHubAgent | 368440 | SmartFile の場合 |
| nrcomgrdki | 368420 | NURILAB |
| nrcomgrdka | 368420 | NURILAB |
| nrpmonki | 368410 | NURILAB |
| nrpq monka. sys | 368410 | NURILAB |
| nravwka | 368400 | NURILAB |
| bhkavki | 368390 | NURILAB |
| bhkavka. sys | 368390 | NURILAB |
| docvmonk 者 | 368380 | NURILAB |
| docvmonk64 | 368380 | NURILAB |
| InvProtectDrv | 368370 | Invincea |
| InvProtectDrv64 | 368370 | Invincea |
| browserMon. sys | 368360 | Adtrustmedia |
| SfdFilter .sys | 368350 | Sandoll 通信 |
| phdcbtdrv .sys | 368340 | PHD Virtual Tech Inc. |
| sysdiag .sys | 368330 | HeroBravo テクノロジ |
| CmdCwagt | 368322 | Comodo Security Solutions Inc. |
| cfrmd. sys | 368320 | Comodo Security Solutions Inc. |
| repdrv | 368310 | ビジョンソリューション |
| repmon | 368300 | ビジョンソリューション |
| cvofflineFlt32 | 368200 | Quantum Corporation。 |
| cvofflineFlt64 | 368200 | Quantum Corporation。 |
| DsDriver .sys | 368100 | ディスクソフトウェアのワープ |
| nlcbhelpx86 | 368000 | NetLib |
| nlcbhelpx64 | 368000 | NetLib |
| nlcbhelpi64 | 368000 | NetLib |
| wbfilter | 367950 | ホワイトボックスのセキュリティ |
| LRAgentMF | 367900 | LogRhythm Inc. |
| Drwebfwflt | 367810 | 医師 Web |
| EventMon. sys | 367800 | 医師 Web |
| dsfltfs .sys | 367760 | Digitalsense Co |
| soidriver .sys | 367750 | Sophos Plc |
| drvhookcsmf | 367700 | GrammaTech, Inc. |
| drvhookcsmf_amd64 | 367700 | GrammaTech, Inc. |
| avipbb .sys | 367600 | AGmbH |
| FileSightMF | 367500 | PA ファイルの視野 |
| csaam .sys | 367400 | Cisco システム |
| FSMon | 367300 | 1mill |
| filefilter. sys | 367100 | 北京 Zhong Jiaxin Computer テクノロジ Co., Ltd. |
| iiscache .sys | 367000 | [Microsoft] |
| nowonmf | 366993 | Diskeeper Corporation |
| dktlfsmf .sys | 366992 | Diskeeper Corporation |
| DKDrv .sys | 366991 | Diskeeper Corporation |
| DKRtWrt-XPSP3 の temp fix | 366990 | Diskeeper Corporation |
| HBFSFltr | 366980 | Diskeeper Corporation |
| xoiv8x64 | 366940 | Arcserve |
| xomfcbt8x64 | 366930 | CA |
| KmxAgent .sys | 366920 | CA |
| KmxFile .sys | 366910 | CA |
| KmxSbx | 366900 | CA |
| PointGuardVistaR32 | 366810 | Futex |
| PointGuardVistaR64 | 366810 | Futex |
| Pointguの場合 | 366800 | Futex |
| PointGuardVista64F | 366800 | Futex |
| vintmfs | 366789 | CondusivTechnologies |
| hiofs .sys | 366782 | Condusiv テクノロジ |
| intmfs | 366781 | CondusivTechnologies |
| excfs | 366780 | CondusivTechnologies |
| zampit_ml | 366700 | Zampit |
| tesxnginx | 366666 | Tencent テクノロジ |
| rflog .sys | 366600 | AppStream, Inc. |
| csmon | 366582 | CyberSight Inc. |
| mumdi | 366540 | ZenmuTech Inc. |
| LivedriveFilter | 366500 | Livedrive Internet Ltd. |
| regmonex .sys | 366410 | Tranxition Corp |
| TXRegMon | 366400 | Tranxition Corp |
| SDVFilter .sys | 366300 | Soliton Systems K.K. |
| eLock2FSCTLDriver | 366210 | これはテクノロジの Inc. です。 |
| msiodrv4 | 366200 | Centennial Software Ltd. |
| mmPsy32 | 366110 | Resplendence プロジェクト |
| mmPsy64 | 366110 | Resplendence プロジェクト |
| rrMon32 | 366100 | Resplendence プロジェクト |
| rrMon64 | 366100 | Resplendence プロジェクト |
| cvsflt | 366000 | 3月の h Software Ltd. |
| ktsyncfsflt | 365920 | KnowledgeTree Inc. |
| nvmon | 365900 | NetVision, Inc. |
| SnDacs | 365810 | の場合 |
| SnExequota | 365800 | の場合 |
| llfilter .sys | 365700 | SecureAxis ソフトウェア |
| hafsnk | 365660 | HA Unix Pt |
| DgeDriver | 365655 | Dell Software Inc. |
| BWFSDrv .sys | 365650 | Quest ソフトウェア Inc. |
| CAADFlt | 365601 | Quest ソフトウェア Inc. |
| QFAPFlt | 365600 | Quest ソフトウェア |
| XendowFLT | 365570 | Credant テクノロジ |
| fmdrive | 365500 | Cigital, Inc. |
| EGMinFlt | 365400 | WhiteCell Software Inc. |
| it2reg | 365315 | Soliton システム |
| it2drv | 365310 | Soliton システム |
| solitkm | 365300 | Soliton システム |
| pgpwdefs .sys | 365270 | Symantec |
| GEProtection. sys | 365260 | Symantec |
| diflt | 365260 | Symantec Corp。 |
| sysMon | 365250 | Symantec |
| ssrfsf | 365210 | Symantec |
| emxdrv2 | 365200 | Symantec |
| reghook .sys | 365150 | Symantec |
| symevnt .sys | 365110 | Symantec |
| spbbcdrv .sys | 365100 | Symantec |
| bhdrvx86 | 365100 | Symantec |
| bhdrvx64 | 365100 | Symantec |
| SISIPSFileFilter | 365010 | Symantec |
| symevent | 365000 | Symantec |
| wrpfv .sys | 364900 | [Microsoft] |
| Upguシャード | 364810 | UpGuard |
| usbl_ifsfltr | 364800 | SecureAxis |
| ntfsf | 364700 | Sun & ムーン |
| BssAudit .sys | 364600 | ByStorm |
| GPMiniFIlter フィルター sys | 364500 | Kalpataru |
| AlfaFF | 364400 | Mg-alfa |
| FSAFilter .sys | 364300 | ScriptLogic |
| GcfFilter .sys | 364200 | GemacmbH |
| FFCFILT.SYS.DATABASES | 364100 | FFC 限定 |
| msnfsflt | 364000 | [Microsoft] |
| mblmon | 363900 | Packeteer |
| amsfilter | 363800 | Axur 情報 (Sec)。 |
| rswctrl. sys | 363713 | Douzone Bizon Co |
| mcstrg .sys | 363712 | Douzone Bizon Co |
| fmkkc | 363711 | Douzone Bizon Co |
| nmlhssrv01 | 363710 | Douzone Bizon Co |
| equ8_helper | 363705 | Int3 Software AB |
| strapvista .sys (廃止) | 363700 | AvSoft テクノロジ |
| SAFE-Agent | 363636 | 安全-Cyberdefense |
| EstPrmon | 363610 | ESTsoft corp。 |
| Estprp-64 ビット | 363610 | ESTsoft corp。 |
| EstRegmon | 363600 | ESTsoft corp。 |
| EstRegp. sys-64 ビット | 363600 | ESTsoft corp。 |
| agfsmon | 363530 | TechnoKom Ltd. |
| NlxFF .sys | 363520 | OnGuard Systems のシステム |
| サハラ | 363511 | Saf の終了 |
| サンタ .sys | 363510 | Saf の終了 |
| vfdrv .sys | 363500 | Viewfinfin |
| topdogfsfilt | 363450 | ManTech |
| xhunter64 | 363400 | Wellbia&#x2024;com |
| アン未確認 | 363390 | Wellbia&#x2024;com |
| AuditFlt | 363313 | Ionx Solutions p |
| SPIMiniFilter | 363300 | ソフトウェアのいいね。 |
| mracdrv .sys | 363230 | メール&#x2024;Ru |
| BEDaisy | 363220 | BattlEye イノベーション |
| Net、Ctrl. sys | 363200 | リンク co。 |
| NetAccCtrl64 | 363200 | リンク co。 |
| hpreg | 363130 | HP |
| qfimdvr .sys | 363120 | Qualys Inc. |
| QDocumentREF. sys | 363110 | BicDroid Inc. |
| dsfemon | 363100 | トポロジ Ltd. |
| AmznMon | 363030 | アマゾンウェブサービス Inc. |
| iothorfs | 363020 | ioScience |
| ctamflt | 363010 | ComTrade |
| psi? sys | 363000 | SharpCrafters |
| QmInspec. sys | 362990 | 北京 QiAnXin Tech。 |
| GagSecurity | 362970 | 北京 Shu Yan サイエンス |
| Cybカーネルトラッカー | 362960 | CyberArk ソフトウェア |
| filemon | 362950 | Temasoft S.R.L. |
| Scaは .sys | 362940 | Sogou Ltd.。 |
| fpifp_minifilter | 362930 | ForcePoint の参照。 |
| klifks | 362902 | Kaspersky ラボ |
| klifaa .sys | 362901 | Kaspersky ラボ |
| Klifsm | 362900 | Kaspersky ラボ |
| nxrmflt | 362860 | NextLabs |
| 大規模な .sys | 362850 | PolyLogyx の場合 |
| AALProtect | 362840 | AlphaAntiLeak |
| egnfsflt | 362830 | Egnyte Inc. |
| RsFlt | 362820 | Redstor 制限 |
| CentrifyFSF | 362810 | Centrify Corp |
| Sefo. sys-Bottom | 362800 | お金 |
| SFPMonitor .sys-Bottom | 362700 | SonicWall Inc. |
| minispy-Bottom | 361000 | [Microsoft] |

## <a name="span-id340000_-_349999__fsfilter_undeletespanspan-id340000_-_349999__fsfilter_undeletespanspan-id340000_-_349999__fsfilter_undeletespan340000---349999-fsfilter-undelete"></a><span id="340000_-_349999__FSFilter_Undelete"></span><span id="340000_-_349999__fsfilter_undelete"></span><span id="340000_-_349999__FSFILTER_UNDELETE"></span>34万-349999: FSFilter の削除の取り消し

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| BSSFlt | 346000 | ブルーシューズソフトウェアの靴 |
| ThinIO | 345900 | ThinScale テクノロジ |
| hmpalert. sys | 345800 | 右へ |
| nsffkmd64 | 345700 | NetSTAR Inc. |
| nsffkmd32 | 345700 | NetSTAR Inc. |
| xbのフィルター (.sys) | 345600 | Zrxb |
| ifileguard. sys | 345500 | I-O DATA DEVICE, INC. |
| undelex32 | 345400 | Resplendence プロジェクト |
| undelex64 | 345400 | Resplendence プロジェクト |
| starmon | 345300 | Kantowitz Engineering, Inc. |
| mxRCycle | 345200 | Avanquest |
| UdFilter .sys | 345100 | Diskeeper Corporation |
| it2prtc | 345040 | Soliton Systems K.K. |
| このようになります。 | 345030 | Soliton Systems K.K. |
| システム | 345020 | Soliton Systems K.K. |
| このようになります。 | 345010 | Soliton Systems K.K. |
| システム | 345000 | Soliton スマート秒 |
| DCVPr .sys | 340700 | セキュリティースター GmbH |

## <a name="span-id320000_-_329998__fsfilter_anti-virusspanspan-id320000_-_329998__fsfilter_anti-virusspanspan-id320000_-_329998__fsfilter_anti-virusspan320000---329998-fsfilter-anti-virus"></a><span id="320000_-_329998__FSFilter_Anti-Virus"></span><span id="320000_-_329998__fsfilter_anti-virus"></span><span id="320000_-_329998__FSFILTER_ANTI-VIRUS"></span>32万-329998: FSFilter ウイルス対策

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| zwPxeSvr .sys | 329330 | SecureLink Inc. |
| Zて Atom. sys | 329320 | SecureLink Inc. |
| wscm. sys | 329310 | 富士通のソーシャルサイエンス |
| IMFFilter .sys | 329300 | IObit 情報技術 |
| CSFlt | 329290 | ConeSecurity Inc. |
| ospfile_mini | 329230 | OKUMA Corp |
| SoftFilterxxx .sys | 329222 | WidgetNuri Corp |
| RansomDefensexxx | 329220 | WidgetNuri Corp |
| RanPodFS | 329210 | システムの管理 |
| ksfsflt | 329200 | 北京の王国 |
| DeepInsFS | 329190 | Deep 性質 |
| AppCheckD .sys | 329180 | CheckMAL Inc. |
| spellmon | 329170 | SpellSecurity |
| ホワイトリスト (d) | 329160 | Meidensha Corp |
| reアク tor. sys | 329150 | Reアク Ta Ltd. |
| SE46Filter | 329140 | テクノロジの対応 |
| FileScan | 329130 | NPcore Ltd. |
| ECATDriver .sys | 329120 | ジャパン |
| pfkrnl | 329110 | FXSEC LTD. |
| E鳥フィルター .sys | 329100 | 非表示のリフレックス |
| b9kernel | 329050 | Bit9 Inc. |
| eeCtrl | 329010 | Symantec |
| 消しゴム .sys (廃止) | 329010 | Symantec |
| SRTSP. sys | 329000 | Symantec |
| SRTSPIT-ia64 システム | 329000 | Symantec |
| SRTSP64.SYS-x64 システム | 329000 | Symantec |
| a2ertpx86 | 328920 | Emsi Software GmbH |
| a2ertpx64 | 328920 | Emsi Software GmbH |
| a2gffx86-x86 | 328910 | Emsi Software GmbH |
| a2gffx64-x64 | 328910 | Emsi Software GmbH |
| a2gffi64-IA64 | 328910 | Emsi Software GmbH |
| a2acc | 328900 | Emsi Software GmbH |
| x64 システムでの a2acc64 | 328900 | Emsi Software GmbH |
| フライトレコーダー | 328850 | Malwarebytes Corp. |
| si32_file | 328810 | Scargo Inc. |
| si64_file | 328810 | Scargo Inc. |
| mbam .sys | 328800 | Malwarebytes Corp. |
| Enigmafilのドライバー (.sys) | 328770 | Enigoft Oft |
| KUBWKSP | 328750 | Netlor SAS |
| hcp_kernel_acq | 328740 | 参照アクションポイント |
| SegiraFlt | 328730 | Segira の場合 |
| wdocsafe | 328722 | Cheetah Mobile Inc. |
| lbprotect | 328720 | Cheetah Mobile Inc. |
| eamonm .sys | 328700 | ESET、spol。 s r.o. |
| klam | 328650 | Kaspersky ラボ |
| MaxProc64 | 328620 | セキュリティで保護されたソフトウェアの最大数 |
| MaxProtector。 sys | 328610 | セキュリティで保護されたソフトウェアの最大数 |
| maxcryptmon | 328601 | セキュリティで保護されたソフトウェアの最大数 |
| SDActMon | 328600 | セキュリティで保護されたソフトウェアの最大数 |
| fileflt | 328540 | Trend Micro Inc. |
| TmEsFlt | 328530 | Trend Micro Inc. |
| TmEyes. sys | 328520 | Trend Micro Inc. |
| tmevtmgr | 328510 | Trend Micro Inc. |
| tmpreflt | 328500 | 加算 |
| vcMFilter .sys | 328400 | SGRI Co., LTD. |
| SAFsFilter | 328300 | ライトスピードシステム Inc. |
| vsepflt | 328200 | VMware, Inc. |
| VFileFilter. sys (名前が変更されました) | 328200 | VMware, Inc. |
| sfavflt | 328130 | テクノロジの sang |
| sfavflt | 328120 | テクノロジの sang |
| drivesentryfilterdriver2lite | 328100 | ドライブエントリ Inc. |
| WdFilter .sys | 328010 | [Microsoft] |
| mpFilter .sys | 328000 | [Microsoft] |
| vrSDetri | 327801 | ETRI |
| vrSDetrix | 327800 | ETRI |
| AhkSvPro .sys | 327720 | Ahkun。 |
| AhkUsbFW. sys | 327710 | Ahkun。 |
| AhkAMFlt | 327700 | Ahkun。 |
| PSINPROC。SYS.DATABASES | 327620 | パンダのセキュリティ |
| PSINFILE。SYS.DATABASES | 327610 | パンダのセキュリティ |
| amfsm .sys-Windows XP/2003 x64 | 327600 | パンダのセキュリティ |
| amm8660-Windows Vista x86 | 327600 | パンダのセキュリティ |
| amm6460-Windows Vista x64 | 327600 | パンダのセキュリティ |
| ADSpiderDoc | 327550 | Digitalonnet |
| BkavAutoFlt | 327542 | Bkav Corporation |
| BkavSdFlt | 327540 | Bkav Corporation |
| easyanticheat | 327530 | EasyAntiCheat ソリューション |
| 5nine. cbt. .sys | 327520 | 5nine ソフトウェア Inc. |
| caavFltr | 327510 | コンピューターのアソシエーション |
| ino_fltr | 327500 | コンピューターのアソシエーション |
| SECOne_USB | 327426 | GRGBanking 機器 |
| SECOne_Proc10 | 327424 | GRGBanking 機器 |
| SECOne_REG10 | 327422 | GRGBanking 機器 |
| SECOne_FileMon10 | 327420 | GRGBanking 機器 |
| WCSDriver | 327410 | ホワイトクラウドのセキュリティ |
| 360qpesv | 327404 | 360ソフトウェア (北京) |
| dsark | 327402 | Qihoo 360 |
| 360avflt | 327400 | Qihoo 360 |
| scifsflt | 327333 | SECUI Corporation |
| ANVfsm .sys | 327310 | Arcdo |
| CDrRSFlt | 327300 | Arcdo |
| mfdriver .sys | 327250 | Imperva Inc. |
| EPSMn .sys | 327200 | 中 |
| VTSysFlt | 327150 | 北京 Venus |
| TesMon. sys | 327130 | Tencent |
| QQSysMonX64 | 327125 | Tencent |
| QQSysMon. sys | 327120 | Tencent |
| TSysCare | 327110 | Shenzhen Tencent コンピューターシステムの企業限定 |
| TFsFlt | 327100 | Shenzhen Tencent コンピューターシステムの企業限定 |
| avmf. sys | 327000 | Authentium |
| BDFileDefend | 326916 | Baidu (北京) |
| BDsdKit .sys | 326914 | Baidu オンラインネットワークテクノロジ (北京) Co。 |
| bd0003 | 326912 | Baidu オンラインネットワークテクノロジ (北京) Co。 |
| Bfilter. sys | 326910 | Baidu (香港) 限定 |
| NeoKerbyFilter | 326900 | NeoAutus |
| egnfsflt | 326830 | Egnyte Inc. |
| RsFlt | 326820 | Redstor 制限 |
| trpmnflt | 326810 | TRAPMINE A.S. |
| PLGFltr | 326800 | Paretologic |
| WrdWizSecure64 | 326730 | WardWiz |
| wrdwizscanner | 326720 | WardWiz |
| AshAvScan .sys | 326700 | Ashampoo GmbH & ・ KG |
| Zyfm | 326666 | ZhengYong InfoTech LTD. |
| csaav. sys | 326600 | Cisco システム |
| oavfm. sys | 326550 | HSM IT-サービス Gmbh |
| SegMD | 326520 | Segurmatica |
| SegMP | 326510 | Segurmatica |
| SegF | 326500 | Segurmatica |
| eeh | 326400 | eEye デジタルセキュリティ |
| eeyehv64 | 326400 | eEye デジタルセキュリティ |
| CpAvFilter .sys | 326311 | CodeProof テクノロジ Inc. |
| CpAvKernel .sys | 326310 | CodeProof テクノロジ Inc. |
| NovaShield | 326300 | テクノロジ、Inc. |
| SheedAntivirusFilterDriver | 326290 | SheedSoft Ltd. |
| bSyirmf | 326260 | BLACKFORT のセキュリティ |
| bSysp .sys | 326250 | BLACKFORT のセキュリティ |
| bSymfdm | 326240 | BLACKFORT のセキュリティ |
| bSywl | 326235 | BLACKFORT のセキュリティ |
| bSyrtm .sys | 326230 | BLACKFORT のセキュリティ |
| bSyaed. sys | 326220 | BLACKFORT のセキュリティ |
| bSyar | 326210 | BLACKFORT のセキュリティ |
| BdFileSpy | 326200 | BullGuard |
| npxgd | 326160 | インカインターネット Co。 |
| npxgd64 | 326160 | インカインターネット Co。 |
| tkpl2k | 326150 | インカインターネット Co。 |
| tkpl2k64 | 326150 | インカインターネット Co。 |
| GKFF .sys | 326140 | インカインターネット Co。 |
| GKFF64 | 326140 | インカインターネット Co。 |
| tkdac2k | 326130 | インカインターネット Co。 |
| tkdacxp | 326130 | インカインターネット Co。 |
| tkdacxp64 | 326130 | インカインターネット Co。 |
| tksp2k | 326120 | インカインターネット Co。 |
| tkspxp | 326120 | インカインターネット Co。 |
| tkspxp64 | 326120 | インカインターネット Co。 |
| tkfsft | 326110 | インカインターネット Co、Ltd. |
| tkfsft64-64 ビット | 326110 | インカインターネット Co、Ltd. |
| tkfsavxp-32 ビット | 326100 | インカインターネット Co、Ltd. |
| tkfsavxp64-64 ビット | 326100 | インカインターネット Co、Ltd. |
| SMDrvNt | 326040 | AhnLab, Inc. |
| ATamptNt | 326030 | AhnLab, Inc. |
| V3Flt2k | 326020 | AhnLab, Inc. |
| V3MifiNt | 326010 | Ahnlab |
| V3Ift2k | 326000 | Ahnlab |
| V3IftmNt (Old name) | 326000 | Ahnlab |
| ArfMonNt .sys | 325990 | Ahnlab |
| AhnRghLh | 325980 | Ahnlab |
| AszFltNt | 325970 | Ahnlab |
| OMFltLh .sys | 325960 | Ahnlab |
| V3Flu2k | 325950 | Ahnlab |
| TfFregNt .sys | 325940 | AhnLab Inc. |
| AdcVcsNT | 325930 | Ahnlab |
| vcdriv | 325820 | Greatsoft Corp. Ltd. |
| vcreg .sys | 325810 | Greatsoft Corp. Ltd. |
| vchle. sys | 325800 | Greatsoft Corp. Ltd. |
| NxFsMon | 325700 | Novatix Corporation |
| AntiLeakFilter | 325600 | 個人開発者 (Soft3304) |
| NanoAVMF | 325510 | パンダソフトウェア |
| shldflt | 325500 | パンダソフトウェア |
| nprosec .sys | 325410 | Norman ASA |
| nregsec .sys | 325400 | Norman ASA |
| issregistry .sys | 325300 | IBM |
| THFilter .sys | 325200 | Sybonic Systems Inc. |
| pervac. sys | 325100 | PerSystems SA |
| avgmfx86 | 325000 | AVG Grisoft |
| avgmfx64 | 325000 | AVG Grisoft |
| avgmfi64 | 325000 | AVG Grisoft |
| avgmfrs (廃止) | 325000 | AVG Grisoft |
| FortiAptFilter .sys | 324930 | For・ et Inc. |
| fortimon2 | 324920 | For・ et Inc. |
| fortirmon .sys | 324910 | For・ et Inc. |
| fortishield .sys | 324900 | For・ et Inc. |
| mscan-rt | 324800 | SecureBrain Corporation |
| sysdiag .sys | 324600 | セキュリティの強化 |
| agentrtm64 | 324510 | WINS CO。 社 |
| rswmon .sys | 324500 | WINS CO。 社 |
| mwfsmfltr | 324420 | マイクロワールドソフトウェアサービス Pvt。 社. |
| gtkdrv | 324410 | GridinSoft の場合 |
| GbpKm .sys | 324400 | ガス Tecnologia |
| crnsysm .sys | 324310 | Coranti Inc. |
| crncache32 | 324300 | Coranti Inc. |
| crncache64 | 324300 | Coranti Inc. |
| システム | 324242 | TEHTRI-セキュリティ |
| drwebfwft | 324210 | 医師 Web |
| DwShield .sys | 324200 | 医師 Web |
| DwShield64 | 324200 | 医師 Web |
| IProtect. sys | 324150 | All Zone Inc. |
| TvFiltr | 324140 | All Zone INC. |
| TvDriver | 324130 | All Zone INC. |
| TvSPFltr | 324120 | All Zone INC. |
| TvPtFile .sys | 324110 | All Zone INC. |
| TvMFltr | 324100 | すべてのゾーン |
| SophosED | 324050 | Sophos |
| SAVOnAccess .sys | 324010 | Sophos |
| savonaccess .sys | 324000 | Sophos |
| sld | 323990 | Sophos |
| OADevice | 323900 | 高さの高さ |
| pwipf6 | 323800 | PWI, Inc. |
| EstRkmon. sys | 323700 | ESTsoft corp。 |
| EstRkr-64 ビット | 323700 | ESTsoft corp。 |
| dwprot | 323610 | 医師 Web |
| Spiderg3 | 323600 | 医師の Web サイト。 |
| STKrnl64 | 323500 | Verdasys Inc. |
| UFDFilter | 323400 | Yoggie |
| SCFltr | 323300 | SecurityCoverage, Inc. |
| fildds. sys | 323200 | Filseclab |
| fsfilter .sys | 323100 | MastedCode Ltd. |
| fpav_rtp | 323000 | f 保護 |
| cwdriver .sys | 322900 | Leith |
| AYFilter .sys | 322810 | ESTsoft |
| Rtw | 322800 | ESTsoft |
| RSRtw. sys | 322790 | ESTsecurity Corp |
| RSPCRtw | 322780 | ESTsecurity Corp |
| HookSys | 322700 | 北京の情報技術 Corporation の制限 |
| snscore .sys | 322600 | S. N 安全 & ソフトウェア |
| ssvhook .sys | 322500 | SecuLution GmbH |
| strapvista .sys | 322400 | AvSoft テクノロジ |
| strapvista64 | 322400 | AvSoft テクノロジ |
| sascan | 322300 | SecureAge テクノロジ |
| savant .sys | 322200 | Savant Protection, Inc. |
| VrARnFlt | 322161 | HAURI |
| VrBBDFlt | 322160 | HAURI |
| vrSDfmx. sys | 322153 | HAURI |
| vrSDfmx. sys | 322152 | HAURI |
| vrSDam .sys | 322151 | HAURI |
| vrSDam .sys | 322150 | HAURI |
| VRAPTFLT | 322140 | HAURI Inc. |
| VrAptDef | 322130 | HAURI |
| VrSdCore .sys | 322120 | HAURI |
| VrFsFtM | 322110 | HAURI |
| VrFsFtMX .sys (AMD64) | 322110 | HAURI |
| vradfil2 | 322100 | HAURI |
| fsgk | 322000 | f-セキュリティ保護 |
| bouncer | 321950 | CoreTrace Corporation |
| PCTCore64 | 321910 | PC ツールの Pty。 社. |
| PCTCore (Old name) | 321910 | PC ツールの Pty。 社. |
| ikfilesec | 321900 | PC ツールの Pty。 社. |
| ZxFsFilt | 321800 | オーストラリアのプロジェクト |
| antispyfilter | 321700 | C-NetMedia Inc. |
| PZDrvXP | 321600 | VisionPower Co., Ltd. |
| ggc | 321510 | クイック回復 TechnologiesPvt。 社. |
| catflt | 321500 | クイック回復 TechnologiesPvt。 社. |
| bdsflt | 321490 | 迅速な回復テクノロジ Pvt。 社. |
| arwflt | 321480 | 迅速な回復テクノロジ Pvt。 社. |
| csagent .sys | 321410 | CrowdStrike Ltd. |
| kmkuflt | 321400 | Komoku Inc. |
| ntguard. sys | 321337 | IKARUS のセキュリティ |
| epdrv .sys | 321320 | McAfee Inc. |
| mfencoas | 321310 | McAfee Inc. |
| mfehidk. sys | 321300 | McAfee Inc. |
| swin .sys | 321250 | McAfee Inc. |
| CyvrFsfd. sys | 321234 | Palo Alto Networks |
| cmdccav .sys | 321210 | Comodo グループ Inc. |
| cmdguard | 321200 | Comodo グループ Inc. |
| K7Sentry | 321100 | K7 Computing Private Ltd. |
| nsminflt | 321050 | NHN |
| nsminflt64 | 321050 | NHN |
| nvcmflt | 321000 | Norman |
| dgsafe | 320950 | 王国 |
| issfltr | 320900 | ISS |
| hbflt | 320840 | BitDefender SRL |
| bdsvm .sys | 320830 | Bitdefender |
| gzflt | 320820 | BitDefender SRL |
| bddevflt | 320812 | BitDefender SRL |
| ignis .sys です | 320811 | BitDefender SRL |
| AVCKF.SYS.DATABASES | 320810 | BitDefender SRL |
| bdfsfltr | 320800 | Softwin |
| bdfm sys | 320790 | Softwin |
| gemma | 320782 | BitDefender SRL |
| Atc | 320781 | BitDefender SRL |
| AVC3.SYS.DATABASES | 320780 | BitDefender SRL |
| TRUFOS.SYS.DATABASES | 320770 | BitDefender SRL |
| aswmonflt | 320700 | Alwil |
| HookCentre | 320602 | G データ |
| Pk、.sys | 320601 | G データ |
| MiniIcpt. sys | 320600 | G データ |
| avgntflt | 320500 | AGmbH |
| klam | 320450 | Kaspersky ラボ |
| klbg | 320440 | Kaspersky |
| kldback. sys | 320430 | Kaspersky |
| kldlinf .sys | 320420 | Kaspersky |
| kldtool .sys | 320410 | Kaspersky |
| klif | 320401 | Kaspersky ラボ |
| klif | 320400 | Kaspersky |
| klam | 320350 | Kaspersky ラボ |
| hsmltwhl | 320340 | Hitachi ソリューション |
| hssfwhl .sys | 320330 | Hitachi ソリューション |
| DeepInsFS | 320320 | Deep 性質 Ltd.。 |
| avfsmn | 320310 | Anvisoft |
| lbd. sys | 320300 | Lavasoft AB |
| pavdrv | 320210 | Panzor サイバーセキュリティ |
| rvsmon | 320200 | CJSC Returnil ソフトウェア |
| WRKrn | 320110 | Webroot Inc. |
| ssfmonm .sys | 320100 | Webroot Software, Inc. |
| vk_fsf | 320050 | AxBx |
| VirtualAgent .sys | 320005 | Symantec |

## <a name="span-id300000_-_309998__fsfilter_replicationspanspan-id300000_-_309998__fsfilter_replicationspanspan-id300000_-_309998__fsfilter_replicationspan300000---309998-fsfilter-replication"></a><span id="300000_-_309998__FSFilter_Replication"></span><span id="300000_-_309998__fsfilter_replication"></span><span id="300000_-_309998__FSFILTER_REPLICATION"></span>30万-309998: FSFilter レプリケーション

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| IntelCAS | 309100 | Intel Corporation |
| mvfs. sys | 309000 | IBM Corporation |
| frxccd | 306000 | FSLogix Inc. |
| fsrecord .sys | 305000 | [Microsoft] |
| InstMon | 304201 | Numecent Inc. |
| StreamingFSD | 304200 | Numecent Inc. |
| ubcminifilterdriver .sys | 304100 | Ullmore Ltd. |
| .sys | 304000 | Legato |
| stfsd | 303900 | 試みテクノロジ |
| xomf | 303800 | CA (XOSOFT) |
| nfid. sys | 303700 | Neverfail Group Ltd. |
| sybfilter .sys | 303600 | Sybase, Inc. |
| rfsfilter .sys | 303500 | Evidian |
| cvmfsj .sys | 303400 | CommVault Systems, Inc. |
| iOraFilter | 303300 | Infonic plc |
| bkbmfd32 (x86) | 303200 | BakBone Software, Inc. |
| bkbmfd64 (x64) | 303200 | BakBone Software, Inc. |
| mblvn | 303100 | Packeteer |
| AV12NFNT | 303000 | AhnLab |
| mDP_win_mini | 302900 | マクロの影響 |
| ctxubs | 302800 | Citrix Systems Inc. |
| rrepfsf | 302700 | Rose-Ems Inc. |
| cbfsfilter2017 | 301900 | スーパー柔軟なソフトウェア |
| AxFilter .sys | 301800 | Axcient Inc. |
| vxfsrep. sys | 301700 | Symantec |
| dellcapfd | 301600 | Dell Inc. |
| Sptres. sys | 301500 | Saf の終了 |
| OfficeBackup .sys | 301400 | お客様のテクノロジ |
| pcvnfilt | 301300 | Blue Coat |
| repdac .sys | 301200 | NSI |
| repkap .sys | 301100 | NSI |
| repdrv | 301000 | NSI |

## <a name="span-id280000_-_289998__fsfilter_continuous_backupspanspan-id280000_-_289998__fsfilter_continuous_backupspanspan-id280000_-_289998__fsfilter_continuous_backupspan280000---289998-fsfilter-continuous-backup"></a><span id="280000_-_289998__FSFilter_Continuous_Backup"></span><span id="280000_-_289998__fsfilter_continuous_backup"></span><span id="280000_-_289998__FSFILTER_CONTINUOUS_BACKUP"></span>28万-289998: FSFilter 連続バックアップ

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| Klcdp | 288900 | Kaspersky ラボ |
| splitinfmon | 288800 | 分割無限大 |
| versamatic | 288700 | Acertant Tech |
| Yfilemon. sys | 288690 | Yarisoft |
| ibac .sys | 288600 | Ide alstor,、 |
| fkdriver | 288500 | Filekeeper |
| AAFileFilter | 288300 | Dell Inc. |
| hyperoo. sys | 288400 | Hyperoo Ltd. |
| HyperBacCA | 285000 | Red Gate Software Ltd. |
| ZMSFsFltr | 284400 | Zenith の InfoTech |
| AlfaSC | 284300 | Alfa Corporation |
| hie_ifs | 284200 | Hie エレクトロニクス, Inc. |
| AAFs. sys | 284100 | AppAssure ソフトウェア |
| defilter .sys (old) | 284000 | [Microsoft] |
| aFsvDrv .sys | 283100 | ITSTATION Inc. |
| tilana | 283000 | Tilana Sys |
| VmDPFilter .sys | 282900 | マクロの影響 |
| LbFilter | 281700 | リンク文 S.r.l. |
| fbsfd .sys | 281600 | Ferro ソフトウェア |
| du、emf | 281500 | S.L.、SPI、 |
| file_tracker | 281420 | Acronis Inc. |
| exbackup. sys | 281410 | Acronis Inc. |
| afcdp. sys | 281400 | Acronis Inc. |
| dcefltr | 281300 | Cofio Software Ltd. |
| ipmrsync_mfilter | 281200 | OpenMars 企業 |
| cascade | 281100 | JP ソフトウェア |
| filearchive. sys | 281000 | コードの分析 |
| syscdp | 280900 | システム OK AB |
| dpm ドライバー (x86) | 280850 | HP |
| dpnedriver64 (x64) | 280850 | HP |
| hpchgflt | 280800 | HP |
| VirtFile | 280700 | Veritas |
| DeqoCPS .sys | 280600 | Deqo |
| LV_Tracker | 280500 | LiveVault |
| cpbak. sys | 280410 | チェックポイントソフトウェア |
| tdmonxp | 280400 | TimeData |
| nvfr_cpd | 280310 | Bakbone Software Inc. |
| nvfr_fdd | 280300 | Bakbone Software Inc. |
| Sptbkp | 280290 | Saf の終了 |
| accessmonitor .sys | 280280 | Briljant Ekonomisystem |

## <a name="span-id260000_-_269998__fsfilter_content_screenerspanspan-id260000_-_269998__fsfilter_content_screenerspanspan-id260000_-_269998__fsfilter_content_screenerspan260000---269998-fsfilter-content-screener"></a><span id="260000_-_269998__FSFilter_Content_Screener"></span><span id="260000_-_269998__fsfilter_content_screener"></span><span id="260000_-_269998__FSFILTER_CONTENT_SCREENER"></span>26万-269998: FSFilter コンテンツスクリーナー

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| Klshadow | 268300 | Kaspersky ラボ |
| TN28 | 268290 | ID 認証技術 |
| PGDriver .sys | 268280 | Avecto Ltd. |
| itseczvdb | 268270 | Innotium Inc. |
| isarsd .sys | 268260 | ISARS |
| zeoscanner | 268255 | PCKeeper |
| fileHiders | 268250 | PCKeeper |
| cbfltfs4-ObserveIT | 268240 | ObserveIT |
| hipara | 268230 | Allsum の場合 |
| このようにしてください。 | 268220 | Alibaba |
| writeGuard. sys | 268210 | TCXA Ltd. |
| KKUDKProtectKer | 268200 | Goldmessage テクノロジ co。 |
| HAWKFIMInt | 268190 | ホークのネットワーク防御 |
| es、ctl | 268180 | EgoSecure GmbH |
| WSguard. sys | 268170 | ワイパー Software UAB |
| Atomizer | 268160 | DragonFlyCodeWorks |
| farwflt | 268150 | Malwarebytes |
| ADSpiderEx2 | 268140 | Digitalonnet |
| sdfilter .sys | 268130 | Igor Zorkov |
| Safe | 268120 | rian@alum.mit.edu |
| mydlpdelete-scanner | 268110 | Medra Teknoloji |
| mydlpscanner. sys | 268100 | Medra Teknoloji |
| hnpro .sys | 268040 | この |
| DLDriverNetMini .sys | 268030 | DeviceLock Inc. |
| ENFFLTDRV | 268020 | Enforcive システム |
| imagentpg. sys | 268012 | インフォ最大 |
| crocopg | 268010 | インフォ最大 |
| sbapifs | 268000 | Sunbelt ソフトウェア |
| H6kernNT | 267920 | H6N テクノロジの提供 |
| SGKD32.SYS.DATABASES | 267910 | NetSection のセキュリティ |
| IccFilter. sys | 267900 | NEC システムテクノロジ |
| tflbc .sys | 267800 | Tani エレクトロニクス Corporation |
| ArmFlt | 267000 | 防御力のあるウイルス対策 |
| WBDrv | 266700 | Axiana の場合 |
| DMSamFilter .sys | 266600 | Digimarc Corp. |
| mumbl | 266540 | ZenmuTech Inc. |
| 5nine. cbt. .sys | 266100 | 5nine ソフトウェア Inc. |
| bsfs. sys | 266000 | クイック回復 TechnologiesPvt。 社.  |
| XXRegSFilter | 265910 | Zhe Jiang Xinxin Software Tech. |
| XXSFilter | 265900 | Zhe Jiang Xinxin Software Tech. |
| AloahaUSBBlocker | 265800 | Wrocklage Intermedia |
| frxdrv .sys | 265700 | FSLogix Inc. |
| FolderSecure .sys | 265600 | セキュリティで保護されたソフトウェアの最大数 |
| XendowFLTC | 265570 | Credant テクノロジ |
| RepDac | 265500 | ビジョンソリューション |
| tbbdriver .sys | 265400 | Tedesi |
| spcgrd | 265300 | 富士通の幅広いソリューション |
| fdtlock .sys | 265250 | 富士通の幅広いソリューション & コンサルティング Inc. |
| ssfFSC .sys | 265200 | SECUWARE S.L. |
| GagSecurity | 265120 | 北京 Shu Yan サイエンス |
| PrintDriver .sys | 265110 | 北京 Shu Yan サイエンス |
| アクティブな | 265100 | Rapidware Pty Ltd. |
| avscan. sys | 265010 | [Microsoft] |
| スキャナー .sys | 265000 | [Microsoft] |
| DI_fs | 264910 | ソフト SB |
| wgnpos. sys | 264900 | Orchestria |
| odfltr | 264810 | NetClean テクノロジ |
| ncpafltr | 264800 | NetClean テクノロジ |
| ct | 264700 | Haute Secure |
| fvefsmf | 264600 | Fortisphere, Inc. |
| ブロック .sys | 264500 | 自律システム限定 |
| csascr sys | 264400 | Cisco システム |
| SymAFR .sys | 264300 | Symantec Corporation |
| cwnep | 264200 | Websense Inc. |
| spywareremover | 264150 | C-Netmedia |
| malwarebot | 264140 | C-Netmedia |
| antispywarebot | 264130 | 2Squared Inc. |
| adwarebot | 264120 | スパイウェア対策 |
| スパイウェア対策 | 264110 | スパイウェア対策 |
| spywarebot | 264100 | C-Netmedia |
| nomp3 | 264000 | Hamish Speirs (プライベート開発者) |
| dlfilter. sys | 263900 | Starfield.html ソフトウェア |
| sifsp .sys | 263800 | セキュリティ保護された諸島テクノロジ LTD. |
| DLFsFlt | 263700 | 中央ツールソフトウェア GmbH |
| SamKeng | 263600 | Syvik Co, Ltd. |
| rml | 263500 | Logis IT Service Gmbh |
| vfsmfd | 263410 | Vontu Inc. |
| vfsmfd | 263400 | Vontu Inc. |
| acfilter .sys | 263300 | Avalere, Inc. |
| psecfilter | 263200 | MDI 研究所、Inc. |
| システムのリダイレクト | 263110 | Soliton システム |
| solitkm | 263100 | Soliton システム |
| ipcfs | 263000 | NetVeda |
| netgateav_access | 262910 | NETGATE 技術。 s.r.o. |
| spyemrg_access | 262900 | NETGATE 技術。 s.r.o. |
| pxrmcet | 262800 | Proxure Inc. |
| EgisTecFF | 262700 | これはテクノロジの Inc. です。 |
| fgcpac | 262600 | Fortres の Corp Corp. |
| saappctl. sys | 262510 | SecureAge テクノロジ |
| sadlp | 262500 | SecureAge テクノロジ |
| CRExecPrev. sys | 262410 | Cybereason |
| PEG2 | 262400 | PE ガード |
| AdminRunFlt | 262300 | Simon ジャービス |
| wvscr | 262200 | Chengdu Wei Tech Inc. |
| psepfilter | 262100 | 絶対ソフトウェア |
| SAMDriver .sys | 262000 | サミット IT |
| emrcore .sys | 261920 | Ivanti Inc. |
| wire_fsfilter | 261910 | ThreatSpike Labs |
| AMFileSystemFilter .sys | 261900 | AppSense Ltd. |
| mtflt | 261880 | mTalos Inc. |
| nxrmflt | 261680 | NextLabs, Inc. |
| oc_fsfilter | 261300 | Raiffeisen Bank Aval |
| hdlpflt | 261200 | McAfee Inc. |
| CCFFilter .sys | 261160 | [Microsoft] |
| cbafilt | 261150 | [Microsoft] |
| SmbBandwidthLimitFilter | 261110 | [Microsoft] |
| DfsrRo | 261100 | [Microsoft] |
| DataScrn | 261000 | [Microsoft] |
| ldusbro .sys | 260900 | LANDesk Inc. |
| FileScreenFilter .sys | 260800 | Veritas |
| cpAcOnPnP | 260720 | conpal GmbH |
| cpsgfsmf | 260710 | conpal GmbH |
| psmmfilter | 260700 | PolyServe |
| pctefa | 260650 | PC ツールの Pty。 社. |
| pctefa64 | 260650 | PC ツールの Pty。 社. |
| symefasi | 260610 | Symantec Corporation |
| symefa | 260600 | Symantec |
| symefa64 | 260600 | Symantec |
| aictracedrv_cs | 260500 | AI コンサルティング |
| DWFIxxxx .sys | 260410 | SciencePark Corporation |
| DWFIxxxx .sys | 260400 | SciencePark Corporation |
| DSDriver .sys | 260330 | ManageEngine Zoho Corp |
| mcfltlab. sys | 260320 | 北京のマイクロ色 |
| FDriver .sys | 260310 | Fox-IT |
| iqpk | 260300 | セキュリティ保護された諸島テクノロジ LTD. |
| VHDFlt | 260240 | Dell |
| VHDFlt | 260230 | Dell |
| VHDFlt | 260220 | Dell |
| VHDFlt | 260210 | Dell |

## <a name="span-id240000_-_249999__fsfilter_quota_managementspanspan-id240000_-_249999__fsfilter_quota_managementspanspan-id240000_-_249999__fsfilter_quota_managementspan240000---249999-fsfilter-quota-management"></a><span id="240000_-_249999__FSFilter_Quota_Management"></span><span id="240000_-_249999__fsfilter_quota_management"></span><span id="240000_-_249999__FSFILTER_QUOTA_MANAGEMENT"></span>24万-249999: FSFilter クォータの管理

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| ntps_qfs | 245100 | NTP ソフトウェア |
| PSSFsFilter | 245000 | PSS システム |
| Sptqmg | 245300 | Saf の終了 |
| storqosflt | 244000 | [Microsoft] |

## <a name="span-id220000_-_229999__fsfilter_system_recoveryspanspan-id220000_-_229999__fsfilter_system_recoveryspanspan-id220000_-_229999__fsfilter_system_recoveryspan220000---229999-fsfilter-system-recovery"></a><span id="220000_-_229999__FSFilter_System_Recovery"></span><span id="220000_-_229999__fsfilter_system_recovery"></span><span id="220000_-_229999__FSFILTER_SYSTEM_RECOVERY"></span>22万-229999: FSFilter システムの回復

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| file_protector | 227000 | Acronis |
| fbwf .sys | 226000 | [Microsoft] |
| Klsysrec | 221500 | Kaspersky ラボ |
| SFDRV.SYS.DATABASES | 221400 | Utixo の場合 |
| sp_prot | 221300 | Xacti Corporation |
| nsfilep .sys | 221200 | Netsupport 制限付き |
| syscow | 221100 | システム OK AB |
| fsredir | 221000 | [Microsoft] |

## <a name="span-id200000_-_209999__fsfilter_cluster_file_systemspanspan-id200000_-_209999__fsfilter_cluster_file_systemspanspan-id200000_-_209999__fsfilter_cluster_file_systemspan200000---209999-fsfilter-cluster-file-system"></a><span id="200000_-_209999__FSFilter_Cluster_File_System"></span><span id="200000_-_209999__fsfilter_cluster_file_system"></span><span id="200000_-_209999__FSFILTER_CLUSTER_FILE_SYSTEM"></span>20万-209999: FSFilter クラスターファイルシステム

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| CVCBT .sys | 203400 | CommVault Systems, Inc. |
| ResumeKeyFilter | 202000 | [Microsoft] |

## <a name="span-id180000_-_189999__fsfilter_hsmspanspan-id180000_-_189999__fsfilter_hsmspanspan-id180000_-_189999__fsfilter_hsmspan180000---189999-fsfilter-hsm"></a><span id="180000_-_189999__FSFilter_HSM"></span><span id="180000_-_189999__fsfilter_hsm"></span><span id="180000_-_189999__FSFILTER_HSM"></span>18万-189999: FSFilter HSM

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| wcifs. sys | 189900 | [Microsoft] |
| prjflt | 189800 | [Microsoft] |
| gameflt | 189750 | [Microsoft] |
| nvmsqrd. sys | 188900 | NVIDIA Corporation |
| RsFlt | 187000 | Redstor 制限 |
| mnefs .sys | 186800 | Nippon Techno Lab |
| Svfsf | 186700 | Spハーソフトテクノロジ |
| uVaultFlt | 186650 | DOR |
| syncmf | 186620 | 酸素クラウド |
| gwmemory. sys | 186600 | Macrotec の場合 |
| cteraflt. sys | 186550 | CTERA Networks Ltd. |
| dbx. sys | 186500 | Dropbox Inc. |
| quaddrasi .sys | 186400 | Quaddra ソフトウェア |
| gdrive .sys | 186300 | 同社 |
| CoreSyncFilter | 186250 | Adobe Systems Inc. |
| EaseTag | 186200 | EaseVault テクノロジ Inc. |
| hcminifilter | 186100 | すばらしい Cloud Inc. |
| PDFsFilter .sys | 186000 | Raxco Sfotware Inc. |
| camino | 185900 | CaminoSoft Corp |
| C2C_AF1R.SYS.DATABASES | 185810 | C2C システム |
| DFdriver .sys | 185800 | DataFirst Corporation |
| amfadrv .sys | 185700 | Quest ソフトウェア Inc. |
| HSMdriver | 185600 | Wim Vervoorn |
| kdfilter | 185555 | Komprise Inc. |
| htdafd. sys | 185500 | ブリッジヘッドソフト |
| odphflt | 180455 | [Microsoft] |
| cldflt | 180451 | [Microsoft] |
| SymHsm | 185400 | Symantec |
| evmf. sys | 185100 | Symantec |
| otfilter .sys | 185000 | 過剰な雰囲気ソフト |
| ithsmdrv | 184900 | IBM |
| MfaFilter .sys | 184800 | Waterford テクノロジ |
| SonyHsmMinifilter | 184700 | Sony Corporation |
| acahsm | 184600 | 自律企業 |
| zlhsm .sys | 184500 | ZL テクノロジ |
| CFileProtect | 184100 | Zhejiang セキュリティ技術 |
| stc_restore_filter | 184000 | StorageCraft テクノロジ |
| dvfilter .sys | 183003 | [Microsoft] |
| システム化 | 183002 | [Microsoft] |
| Changetracker. sys | 183001 | [Microsoft] |
| Fer. sys | 183000 | [Microsoft] |
| hsmcdpflt | 182700 | Metalogix |
| archivmgr | 182690 | Metalogix |
| ntps_oddm | 182600 | NTP ソフトウェア |
| XDFileSys | 182500 | XenData 制限あり |
| upmjit. sys | 182400 | Citrix システム |
| AtmosFS | 182310 | EMC Corporation |
| DxSpy. sys | 182300 | EMC Software Inc. |
| car_hsmflt | 182200 | Caringo, Inc. |
| BRDriver .sys | 182100 | BitRaider |
| BRDriver64 | 182100 | BitRaider |
| autnhsm | 182000 | 自律企業 |
| cthsmflt | 181970 | ComTrade |
| NxMini | 181900 | NEXSAN 製 |
| neuflt | 181818 | NeuShield |
| npfdaflt. sys | 181800 | Mimosa Systems Inc. |
| AppStream .sys | 181700 | AppStream, Inc. |
| HPEDpHsmX64 | 181620 | ヒューレットパッカード, Co. |
| HPArcHsmX64 | 181610 | ヒューレットパッカード, Co. |
| hphsmflt | 181600 | ヒューレットパッカード, Co. |
| cparchsm | 181610 | マイクロフォーカス |
| RepHsm .sys | 181500 | ソフトウェア, Inc. を再利用します。 |
| RepSIS | 181490 | ソフトウェアの再利用 |
| SquashCompressionFsFilter | 181410 | スカッシュ圧縮 |
| GXHSM .sys | 181400 | Commvault Systems, Inc. |
| EdsiHsm .sys | 181300 | Enterprise Data Solutions, Inc. |
| BkfMap | 181200 | データストレージグループ |
| hsmfilter | 181100 | GRAU Data Storage AG |
| mwilcflt | 181020 | Moonwalk Universal P/L |
| mwilsflt | 181010 | Moonwalk Universal P/L |
| mwidmflt | 181000 | Moonwalk Universal P/L |
| HcpAwfs | 181960 | Hitachi データシステム |
| sdrefltr | 180950 | Hitachi データシステム |
| fltasm | 180900 | グローバル360 |
| cnet_hsm | 180850 | Carroll-Net Inc. |
| pntvolflt | 180800 | ソフトウェア & システムのポイント |
| appxstrm | 180710 | [Microsoft] |
| wimmount | 180700 | [Microsoft] |
| hsmflt | 180600 | [Microsoft] |
| dfsrflt | 180500 | [Microsoft] |
| Storagesyncguard.sys | 180465 | [Microsoft] |
| Storagesync.sys | 180460 | [Microsoft] |
| 重複除去. sys | 180450 | [Microsoft] |
| dfmflt | 180410 | [Microsoft] |
| sis .sys | 180400 | [Microsoft] |
| rbt_wfd | 180300 | Riverbed テクノロジ、Inc. |

## <a name="span-id170000_-_174999__fsfilter_imaging_ex_zipspanspan-id170000_-_174999__fsfilter_imaging_ex_zipspanspan-id170000_-_174999__fsfilter_imaging_ex_zipspan170000---174999-fsfilter-imaging-ex-zip"></a><span id="170000_-_174999__*FSFilter_Imaging_(ex:_.ZIP)"></span><span id="170000_-_174999__*fsfilter_imaging_(ex:_.zip)"></span><span id="170000_-_174999__*FSFILTER_IMAGING_(EX:_.ZIP)"></span>17万-174999: * FSFilter Imaging (例:ZIP

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| pfmfs_???.sys.databases | 172100 | Pismo Technic Inc. |
| virtual_file | 172000 | Acronis |
| Wimfltr.sys | 170500 | [Microsoft] |

## <a name="span-id160000_-_169999__fsfilter_compressionspanspan-id160000_-_169999__fsfilter_compressionspanspan-id160000_-_169999__fsfilter_compressionspan160000---169999-fsfilter-compression"></a><span id="160000_-_169999__FSFilter_Compression"></span><span id="160000_-_169999__fsfilter_compression"></span><span id="160000_-_169999__FSFILTER_COMPRESSION"></span>16万-169999: FSFilter 圧縮

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| CmgFFC | 166000 | Credant テクノロジ |
| .sys を圧縮する | 165000 | [Microsoft] |
| cmpflt | 162000 | [Microsoft] |
| IridiumIO | 161700 | # O |
| logcompressor. sys | 161600 | VelociSQL Inc. |
| GcfFilter .sys | 161500 | GemacmbH |
| ssddoubler | 161400 | Sinan Karaca |
| Sptcmp | 161300 | Saf の終了 |
| wimfsf | 161000 | [Microsoft] |
| GEFCMP .sys | 160100 | Symantec |

## <a name="span-id140000_-_149999__fsfilter_encryptionspanspan-id140000_-_149999__fsfilter_encryptionspanspan-id140000_-_149999__fsfilter_encryptionspan140000---149999-fsfilter-encryption"></a><span id="140000_-_149999__FSFilter_Encryption"></span><span id="140000_-_149999__fsfilter_encryption"></span><span id="140000_-_149999__FSFILTER_ENCRYPTION"></span>14万-149999: FSFilter の暗号化

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| FJSeparettiFilterRamMon | 149100 | 富士通限定 |
| psatfilter. sys | 149050 | ProYuga |
| RdFilter .sys | 149040 | CyberEye Research Labs |
| gisfile_decryption | 149030 | 中国の通信 |
| TIFSFilter .sys | 149020 | SG Corporation |
| OsrDt2 | 149010 | 情報セキュリティ Corp |
| EasyKryptMF | 149000 | SoftKrypt の場合 |
| 南京錠 (.sys) | 148910 | IntSoft Inc. |
| ffecore | 148900 | Winmagic |
| fangcloud .sys | 148860 | Hangzhou Yifangyun |
| klvfs | 148810 | Kaspersky ラボ |
| Klfle | 148800 | Kaspersky ラボ |
| ISFP .sys | 148701 | アルプスのシステム統合 |
| ISIRM | 148700 | アルプスのシステム統合 CO。 |
| ASUSSecDrive .sys | 148650 | ASUS |
| ABFilterDriver .sys | 148640 | AlertBoot |
| QDocumentFSF | 148630 | BicDroid Inc. |
| bfusbenc | 148620 | bitFence Inc. |
| sztgbfsf | 148610 | 安全です。 |
| mwIPSDFilter | 148600 | これはテクノロジの Inc. です。 |
| csccvdrv | 148500 | Computer サイエンス Corporation |
| aefs .sys | 148400 | Angelltech Corporation Xi'an |
| VTEFsFlt | 148374 | EsComputer Corp |
| IWCSEFlt | 148300 | InfoWatch |
| GDDmk | 148250 | G データソフトウェア AG |
| clcxcore .sys | 148210 | AFORE ソリューション Inc. |
| OrisLPDrv .sys | 148200 | CGS 発行技術 |
| nlemsys | 148100 | NETLIB |
| prvflder | 148000 | [Microsoft] |
| ssefs | 147900 | SecuLution GmbH |
| SePSed | 147800 | Humming Head, Inc. |
| dlmfencx .sys | 147700 | Data Encryption Ltd. |
| SkyDEnc | 147620 | スカイ Co Ltd. |
| psgcrypt | 147610 | Yokogawa R & L Corp |
| bbfsflt | 147600 | Bloombase |
| qx10efs | 147500 | Quixxant |
| MEfefs .sys | 147400 | Eruces Inc. |
| medlpflt | 147310 | チェックポイントソフトウェアテクノロジ Ltd. |
| dsfa .sys | 147308 | チェックポイントソフトウェアテクノロジ Ltd. |
| Snicrpt | 147300 | Systemneeds 必要性, Inc. |
| iCrypt | 147200 | I-O DATA DEVICE, INC. |
| xdrmflt | 147100 | bluefinsystems |
| dyFsFilter .sys | 147000 | Scrypto メディア |
| thinairwin | 146960 | シン・ Inc. |
| UcaDataMgr | 146950 | AppSense Ltd. |
| zesocc | 146900 | 社 |
| mfprom .sys | 146800 | McAfee Inc. |
| MfeEEFF | 146790 | McAfee Inc. |
| 整合性 (.sys) | 146700 | TianYu ソフトウェア |
| leofs .sys | 146600 | Leotech |
| autocryptater sys | 146500 | Richard Hagen |
| WavxDMgr | 146400 | Scott Cochrane |
| eedmkxp32 | 146300 | Entrust |
| SbCe | 146200 | SafeBoot |
| iSharedFsFilter | 146100 | Packeteer Inc. |
| dlrmenc | 146010 | DESlock |
| dlmfenc | 146000 | DESlock |
| aksdf .sys | 145900 | Aladdin ナレッジシステム |
| DDSFilter .sys | 145800 | WuHan Forworld ソフトウェア |
| SecureShield .sys | 145700 | HMI |
| AifaFE | 145600 | Mg-alfa |
| GBFsMf .sys | 145500 | GreenBorder |
| jmefs .sys | 145400 | 上海 Elec |
| emugufs | 145333 | Emugu Secure FS |
| VFDriver .sys | 145300 | R システム |
| IntelDG | 145250 | Intel Corporation |
| システム | 145240 | Randtronics Pty |
| EVSDecrypt64 | 145230 | Fortium Technologies Ltd. |
| skycryptorencfs | 145220 | Onecryptor CJSC。 |
| AisLeg | 145210 | 情報セキュリティの保証 |
| windtalk | 145200 | Hyland ソフトウェア |
| TeamCryptor | 145190 | iTwin Pte。 社. |
| CVDLP. sys | 145180 | CommVault Systems, Inc. |
| 5nine. 暗号化システム | 145170 | 5nine ソフトウェア Inc. |
| ctpfile | 145160 | 北京 Wondersoft テクノロジ Co。 |
| システム | 145150 | IBM 日本 |
| tsdlp. sys | 145140 | Forware |
| KCDriver .sys | 145130 | Tallegra Ltd. |
| CmgFFE .sys | 145120 | Credant テクノロジ |
| fgcenc | 145110 | Fortres の Corp Corp. |
| sview | 145100 | Cinea |
| TalkeyFilterDriver | 145040 | myTALKEY s.r.o. |
| FedsFilterDriver .sys | 145010 | 物理的な光の Corp |
| stocc | 145000 | Senforce テクノロジ |
| SnEfs | 144900 | の場合 |
| ewSecureDox | 144800 | Echoworx Corporation |
| osrdmk | 144700 | OSR オープンシステムリソース, Inc. |
| uldcr. sys | 144600 | NCR 財務ソリューション |
| Tkefsxp .sys-32 ビット | 144500 | インカインターネット Co、Ltd. |
| Tkefsxp64-64 ビット | 144500 | インカインターネット Co、Ltd. |
| Nml、.sys | 144400 | NEC システムテクノロジ、Ltd. |
| % Crypt | 144300 | Soliton Systems K.K. |
| IngDmk | 144200 | Ingrian Networks, Inc. |
| llenc | 144100 | SecureAxis ソフトウェア |
| SecureData. sys | 144030 | SecureAge テクノロジ |
| lockcube. sys | 144020 | SecureAge テクノロジの Pte Ltd. |
| sdmedia .sys | 144010 | SecureAge テクノロジ |
| mysdrive | 144000 | SecureAge テクノロジ |
| Filの Mor .sys | 143900 | モバイルアーマー |
| VSTXEncr | 143800 | VIA Technologies, Inc. |
| dgdmk | 143700 | Verdasys Inc. |
| shandy | 143600 | Saf end Ltd. |
| C2knet | 143520 | Secuware |
| C2kdef | 143510 | Secuware |
| ssfFS | 143500 | SECUWARE S.L. |
| PISRFE | 143400 | Jilin の IT 共同。 |
| bapfecre | 143300 | BitArmor システム、Inc. |
| 中 SD | 143200 | cihosoft |
| Fcfileio sys | 143100 | Brainzsquare, Ltd. |
| cpdrm. sys | 143000 | Pikewerks |
| vmfiltr .sys | 142900 | Vormetric Inc. |
| VFSEnc. sys | 142811 | Symantec |
| pgpfs .sys | 142810 | Symantec |
| システム | 142800 | Symantec |
| TmFileEncDmk | 142700 | Trend Micro Inc. |
| cpefs .sys | 142600 | 暗号化-Pro |
| dekfs .sys | 142500 | KasherLab co., ltd. |
| qlockfilter .sys | 142400 | Binqsoft Inc. |
| RRFilterDriverStack_d3 | 142300 | 合理的に保持 |
| cve. sys | 142200 | 絶対ソフトウェア Corp。 |
| spcflt | 142100 | 富士通 BSC Inc. |
| ldsecusb .sys | 142000 | LANDesk Inc. |
| fencr sys | 141900 | SODATSW spol。 s.r.o. |
| RubiFlt | 141800 | Hitachi |
| mfild sys | 141660 | Penta セキュリティシステム |
| cbfsfilter2017 | 141635 | オートマトン Inc. |
| cbfsfilter2017 | 141634 | オートマトン Inc. |
| cbfsfilter2017 | 141633 | オートマトン Inc. |
| cbfsfilter2017 | 141632 | オートマトン Inc. |
| cbfsfilter2017 | 141631 | オートマトン Inc. |
| cbfsfilter2017 | 141630 | オートマトン Inc. |
| TypeSquare | 141620 | Morisawa inc. |
| xbdocfilter .sys | 141610 | Zrxb |
| EVSDecrypt32 | 141600 | Fortium Technologies Ltd. |
| EVSDecrypt64 | 141600 | Fortium Technologies Ltd. |
| EVSDecryptia64 | 141600 | Fortium Technologies Ltd. |
| SophosDt2 | 141510 | Sophos Plc |
| afdriver .sys | 141500 | ATUS テクノロジの方法 |
| TrivalentFSFltr | 141430 | サイバーに依存 |
| CmdMnEfs .sys | 141420 | Comodo のセキュリティ |
| DWENxxxx .sys | 141410 | SciencePark Corporation |
| DWENxxxx .sys | 141400 | SciencePark Corporation |
| hdFileSentryDrv32 | 141300 | He/g の防御 |
| hdFileSentryDrv64 | 141300 | He/g の防御 |
| CovertxFilter .sys | 141240 | マイクロフォーカス |
| cplcdt2 | 141230 | conpal GmbH |
| asCryptoFilter .sys | 141220 | 適用されたセキュリティ GmbH |
| NetCryptKR | 141210 | NetCrypt Pty Ltd. |
| BHFilter | 141200 | スピアソリューション |
| Filecrypt | 141100 | [Microsoft] |
| http.sys の暗号化 | 141010 | [Microsoft] |
| swapBuffers. sys | 141000 | [Microsoft] |

## <a name="span-id130000_-_139999__fsfilter_virtualizationspanspan-id130000_-_139999__fsfilter_virtualizationspanspan-id130000_-_139999__fsfilter_virtualizationspan130000---139999-fsfilter-virtualization"></a><span id="130000_-_139999__FSFilter_Virtualization"></span><span id="130000_-_139999__fsfilter_virtualization"></span><span id="130000_-_139999__FSFILTER_VIRTUALIZATION"></span>13万-139999: FSFilter 仮想化

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| Klvirt | 138100 | Kaspersky ラボ |
| VMagic .sys | 138050 | AI コンサルティング |
| GetSAS .sys | 138040 | SAS 協会 Inc. |
| rqtNos | 138030 | Reアク Ta Ltd. |
| HIPS64 | 138020 | Recrypt の場合 |
| frxdrv .sys | 138010 | FSLogix Inc. |
| vzdrv .sys | 138000 | Altiris |
| sffsg .sys | 137990 | ヒトデ Storage Corp |
| AppStream .sys | 137920 | Symantec Corporation |
| Rasm | 137915 | OpDesk Inc. |
| boxifier | 137910 | Kenubi |
| xorw .sys | 137900 | CA (XOsoft) |
| ctlua | 137800 | B.V. |
| fgccow | 137700 | Fortres の Corp Corp. |
| aswSnx .sys | 137600 | ALWIL ソフトウェア |
| AppIsoFltr | 137500 | カーネルドライバー |
| ptcvfsd | 137400 | PTC |
| BDSandBox .sys | 137300 | BitDefender SRL |
| sxfpss-virt | 137200 | Skanix |
| DKRtWrt | 137100 | Diskeeper Corporation |
| ivm .sys | 137000 | RingCube テクノロジ |
| ivm .sys | 136990 | Citrix システム |
| dtiof .sys | 136900 | Instavia Software Inc. |
| NxTopCP | 136800 | 仮想 Ccomputer Inc. |
| svdriver .sys | 136700 | VMware, Inc. |
| unifltr | 136600 | Unidesk |
| unidrive (名前の変更) | 136600 | Unidesk |
| unirsd. sys | 136600 | Unidesk |
| ive | 136500 | TrendMicro Inc. |
| odamf | 136450 | Sony Corporation |
| SrMxfMf | 136440 | Sony Corporation |
| pszmf. sys | 136430 | Sony Corporation |
| sxsudfmf | 136410 | Sony Corporation |
| vfammf | 136400 | Sony Corporation |
| VHDFlt | 136240 | Dell |
| VHDFlt | 136230 | Dell |
| VHDFlt | 136220 | Dell |
| VHDFlt | 136210 | Dell |
| ncfsfltr | 136200 | NComputing Inc. |
| cmdguard | 136100 | COMODO Security Solutions Inc. |
| hpfsredir | 136000 | HP |
| svhdxflt | 135100 | [Microsoft] |
| luafv .sys | 135000 | [Microsoft] |
| ivm .sys | 134000 | RingCube テクノロジ |
| ivm .sys | 133990 | Citrix システム |
| frxdrvvt | 132700 | FSLogix Inc. |
| pfmfs_???.sys.databases | 132600 | Pismo Technic Inc. |
| Stcvhdmf | 132600 | StorageCraft Tech Corp |
| appdrv01 | 132500 | 保護テクノロジ |
| virtual_file | 132400 | Acronis |
| pdiFsFilter | 132300 | 位 Data Inc. |
| avgvtx86 | 132200 | 平均テクノロジ CS-CZ |
| avgvtx64 | 132200 | 平均テクノロジ CS-CZ |
| DataNet_Driver | 132100 | AppSense Ltd. |
| EgenPage .sys | 132000 | Eebcdic a, Inc. |
| unidrive-old | 131900 | Unidesk |
| ivm. sys. old | 131800 | RingCube テクノロジ |
| XiaobaiFsR | 131710 | SHENZHEN UNNOO LTD. |
| XiaobaiFs | 131700 | SHENZHEN UNNOO LTD. |
| iotfsflt | 131600 | IO タービン Inc. |
| mhpvfs. sys | 131500 | Wunix の制限 |
| svdriver .sys | 131400 | SnapVolumes Inc. |
| Sptvrt | 131300 | Saf の終了 |
| rswf のアンチ .sys | 131210 | Panzor サイバーセキュリティ |
| aicvirt | 131200 | AI コンサルティング |
| sfo .sys | 130100 | [Microsoft] |
| DeVolume | 13万 | [Microsoft] |

## <a name="span-id120000_-_129999__fsfilter_physical_quota_managementspanspan-id120000_-_129999__fsfilter_physical_quota_managementspanspan-id120000_-_129999__fsfilter_physical_quota_managementspan120000---129999-fsfilter-physical-quota-management"></a><span id="120000_-_129999__FSFilter_Physical_Quota_management"></span><span id="120000_-_129999__fsfilter_physical_quota_management"></span><span id="120000_-_129999__FSFILTER_PHYSICAL_QUOTA_MANAGEMENT"></span>12万-129999: FSFilter 物理クォータ管理

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| クォータ. sys | 125000 | [Microsoft] |
| qafilter | 124000 | Veritas |
| DroboFlt | 123900 | データロボット |

## <a name="span-id100000_-_109999__fsfilter_open_filespanspan-id100000_-_109999__fsfilter_open_filespanspan-id100000_-_109999__fsfilter_open_filespan100000---109999-fsfilter-open-file"></a><span id="100000_-_109999__FSFilter_Open_File"></span><span id="100000_-_109999__fsfilter_open_file"></span><span id="100000_-_109999__FSFILTER_OPEN_FILE"></span>10万-109999: FSFilter 開いているファイル

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| insyncmf | 105000 | InSync |
| SPILock8 | 100900 | ソフトウェアのいいね。 |
| Klbackupflt | 100800 | Kaspersky |
| repkap | 100700 | ビジョンソリューション |
| symrg | 100600 | Symantec |
| adsfilter | 100500 | PolyServ |

## <a name="span-id80000_-_89999__fsfilter_security_enhancerspanspan-id80000_-_89999__fsfilter_security_enhancerspanspan-id80000_-_89999__fsfilter_security_enhancerspan80000---89999-fsfilter-security-enhancer"></a><span id="80000_-_89999__FSFilter_Security_Enhancer"></span><span id="80000_-_89999__fsfilter_security_enhancer"></span><span id="80000_-_89999__FSFILTER_SECURITY_ENHANCER"></span>8万-89999: FSFilter セキュリティ言え

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| psprotf | 88210 | Panzor サイバーセキュリティ |
| システム (l) | 88100 | Randtronics Pty |
| dsbwnck | 88000 | Easy Solution Inc. |
| cbfsfilter2017 | 87910 | オートメーション |
| cbfsfilter2017 | 87909 | オートマトン Inc. |
| cbfsfilter2017 | 87908 | オートマトン Inc. |
| cbfsfilter2017 | 87907 | オートマトン Inc. |
| cbfsfilter2017 | 87906 | オートマトン Inc. |
| cbfsfilter2017 | 87905 | オートマトン Inc. |
| cbfsfilter2017 | 87904 | オートマトン Inc. |
| cbfsfilter2017 | 87903 | オートマトン Inc. |
| cbfsfilter2017 | 87902 | オートマトン Inc. |
| cbfsfilter2017 | 87901 | オートマトン Inc. |
| cbfsfilter2017 | 87900 | オートマトン Inc. |
| rsbfsfilter .sys | 87800 | Corel Corporation |
| hsmltflt | 87720 | Hitachi ソリューション |
| hssfflt. sys | 87710 | Hitachi ソリューション |
| acmnflt | 87708 | Hitachi ソリューション |
| ACSKFFD .sys | 87700 | Hitachi ソリューション |
| MyDLPMF | 87600 | Comodo グループ Inc. |
| ScuaRaw | 87500 | Scua Seguran&#231;a da&#231;&#227;、o |
| HDSFilter .sys | 87400 | NeoAutus オートメーションシステム |
| ikfsmflt | 87300 | IronKey Inc. |
| Klsec | 87200 | Kaspersky ラボ |
| XtimUSBFsFilterDrv .sys | 87190 | Dalian CP-SDT |
| RGFLT_FM | 87180 | Hauri inc. |
| flockflt | 87170 | Ahranta Inc. |
| ZdCore .sys | 87160 | Zends の技術的ソリューション |
| dcrypt | 87150 | ReactOS Foundation |
| hpradeo | 87140 | Pradeo |
| SDFSAGDRV。SYS.DATABASES | 87130 | アルプスのシステム統合 CO。 |
| SDFSDEVFDRV。SYS.DATABASES | 87120 | アルプスのシステム統合 CO。 |
| SDIFSFDRV。SYS.DATABASES | 87110 | アルプスのシステム統合 CO。 |
| SDFSFDRV。SYS.DATABASES | 87100 | アルプスのシステム統合 CO。 |
| CModule .sys | 87070 | Zhejiang セキュリティ技術 |
| HHRRPH | 87010 | H + H Software GmbH |
| HHVolFltr | 87000 | H + H Software GmbH |
| SbieDrv .sys | 86900 | Sandboxie L. T. d. |
| assetpro | 86800 | pyaprotect&#x2024;com |
| dlp | 86700 | Tellus ソフトウェア |
| .eps | 86600 | Lumension のセキュリティ |
| RapportPG64 | 86500 | Trusteer |
| amminifilter フィルター sys | 86400 | AppSense |
| Sniflt | 86300 | Systemneeds 必要性, Inc. |
| SecFile .sys | 86200 | Design Inc. によるセキュリティ保護 |
| philly | 86110 | triCerat Inc. |
| reggy | 86100 | triCerat Inc. |
| cygfilt | 86000 | Livegrid 組み込み |
| 事前起動 | 85900 | D3L |
| csareg .sys | 85810 | Cisco システム |
| csaenh | 85800 | Cisco システム |
| asEpsDrv .sys | 85750 | ASHINI のコロケーション。 |
| CIDACL | 85700 | GE 航空 (Digital Systems Germantown) |
| CVDLP. sys | 85610 | CommVault Systems, Inc. |
| QGPEFlt | 85600 | Quest ソフトウェア |
| Dre | 85500 | CA |
| vracfil2 | 85400 | HAURI |
| TFsDisk .sys | 85300 | Teruten |
| rcMiniDrv | 85200 | REDGATE CO., LTD. |
| SnMc5xx | 85100 | の場合 |
| FSPFltd. sys | 85010 | Mg-alfa |
| Aifが p. .sys | 85000 | Mg-alfa |
| EsAccCtlFE | 84901 | EgoSecure GmbH |
| DpAccCtl. sys | 84900 | Softbroker GmbH |
| privman. sys | 84800 | BeyondTrust |
| eumntvol | 84700 | Eugrid Inc. |
| SoloEncFilter | 84600 | Soliton システム |
| sbfilter | 84500 | UC4 のソフトウェア |
| cposfw .sys | 84450 | チェックポイントソフトウェアテクノロジ Ltd. |
| vsdatant. sys | 84400 | Zone Labs のお金 |
| SePnet | 84350 | Humming Head, Inc. |
| Seて d. .sys | 84340 | Humming Head, Inc. |
| SePpld | 84330 | Humming Head, Inc. |
| SePfsd | 84320 | Humming Head, Inc. |
| SePwld | 84310 | Humming Head, Inc. |
| SePprd | 84300 | Humming Head, Inc. |
| InPFlter .sys | 84200 | Humming Head, Inc. |
| CProCtrl. sys | 84100 | 暗号化-Pro |
| spyshelter | 84000 | Datpol |
| clpinspprot | 83900 | 情報技術会社 Ltd. |
| uvmfsflt | 83376 | NEC Corporation  |
| ProtectIt | 82373 | テラバイトの Inc. |
| dguard. sys | 82300 | Dmitry Varshavsky |
| NSUSBStorageFilter | 82200 | NetSupport Ltd. |
| RMSEFFMV。SYS.DATABASES | 82100 | CJSC Returnil ソフトウェア |
| BoksFLAC | 82000 | Fox テクノロジ |
| cpAcOnPnP | 81910 | conpal GmbH |
| cpsgfsmf | 81900 | conpal GmbH |
| ndevsec .sys | 81800 | Norman ASA |
| ViewIntus_RTDG | 81700 | Pentego Technologies Ltd. |
| エアロック .sys | 81630 | エアロックデジタル Pty Ltd. |
| zam .sys | 81620 |  |
| ANXfsm | 81610 | Arcdo |
| CDrSDFlt | 81600 | Arcdo |
| crnselfdefence32 | 81500 | Coranti Inc. |
| crnselfdefence64 | 81500 | Coranti Inc. |
| zlock_drv | 81400 | セキュリティ |
| f101fs | 81300 | Fortres の Corp Corp. |
| sysgar | 81200 | 中核データ回復 |
| EmbargoM | 81100 | ScriptLogic |
| ngssdef | 81050 | Wontok Inc. |
| ssb | 81041 | Wontok Inc. |
| regflt | 81040 | Wontok Inc. |
| fsds2a | 81000 | Splitstreem Ltd. |
| csacentr. sys | 80900 | Cisco システム |
| ScvFLT50 | 80850 | Secuve Ltd. |
| paritydriver .sys | 80800 | Bit9, Inc. |
| nkfsprot | 80710 | Konneka |
| nkprot | 80700 | KONNEKA 情報テクノロジ |
| acpadlock | 80691 | IntSoft Co |
| ksmf .sys | 80690 | IntSoft Co |
| http.sys | 80680 | CrowdStrike |
| SophosED | 80670 | Sophos |
| jazzfile .sys | 80660 | ジャズネットワーク |
| SMXFs. sys | 80500 | OSR |

## <a name="span-id60000_-_69999__fsfilter_copy_protectionspanspan-id60000_-_69999__fsfilter_copy_protectionspanspan-id60000_-_69999__fsfilter_copy_protectionspan60000---69999-fsfilter-copy-protection"></a><span id="60000_-_69999__FSFilter_Copy_Protection"></span><span id="60000_-_69999__fsfilter_copy_protection"></span><span id="60000_-_69999__FSFILTER_COPY_PROTECTION"></span>6万-69999: FSFilter のコピー保護

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| d3clock | 67000 | D3CRYPT3D の場合 |
| cbfltfs4 | 66500 | I3D テクノロジ Inc. |
| CkProcess | 66100 | KASHU SYSTEM DESIGN INC. |
| dlmfprot | 66000 | データの暗号化 Sys |
| baprtsef | 65700 | BitArmor システム、Inc. |
| sxfpss | 65600 | Skanix |
| rgasdev | 65500 | Macrovision |
| SkyFPDrv | 65410 | 空のコロケーション。 |
| SkyLWP | 65400 | 空のコロケーション。 |
| SnEraser ゴム | 65300 | の場合 |
| vfilter .sys | 65200 | RSJ Software GmbH |
| COGOFlt32 | 65100 | Fortium Technologies Ltd. |
| COGOFlt64 | 65100 | Fortium Technologies Ltd. |
| COGOFLTia64 | 65100 | Fortium Technologies Ltd. |
| 削除機能 | 65000 | [Microsoft] |
| BRDriver .sys | 64000 | BitRaider の場合 |
| BRDriver64 | 64000 | BitRaider の場合 |
| X7Ex | 62500 | Exent Technologies Ltd. |
| LibertyFSF | 62300 | Bayalink ソリューション共同 |
| axfsdrv2 | 62100 | Axence ソフトウェア Inc. |
| sds | 62000 | 送信ソフトウェア |
| TotalSystemAuditor .sys | 61600 | ANRC のオンライン |
| MBAMApiary .sys | 61500 | Malwarebytes Corp. |
| WA_FSW | 61400 | Programas Admin Aci&#243;n y Mejoramiento |
| ViewIntus_RTAS | 61300 | Pentego テクノロジ |
| tffac .sys | 61200 | 東芝 Corporation |
| tccp .sys | 61100 | TrusCont Ltd. |
| KomFS | 61000 | KOM ネットワーク |

## <a name="span-id40000_-_49999__fsfilter_bottomspanspan-id40000_-_49999__fsfilter_bottomspanspan-id40000_-_49999__fsfilter_bottomspan40000---49999-fsfilter-bottom"></a><span id="40000_-_49999__FSFilter_Bottom"></span><span id="40000_-_49999__fsfilter_bottom"></span><span id="40000_-_49999__FSFILTER_BOTTOM"></span>4万-49999: 下位の FSFilter

| ミニ                  | 対地 | Company                                 |
------------------------------|----------|-----------------------------------------|
| RMPFileMounter | 48000 | ManageEngine Zoho |
| cbfsfilter2017 | 47400 | 12d Synergy |
| pfmfs_???.sys.databases | 47300 | Pismo Technic Inc. |
| DLDriverMiniFlt | 47200 | DeviceLock Inc. |
| hsmltlib | 47110 | Hitachi ソリューション |
| hskdlib. sys | 47100 | Hitachi ソリューション |
| acmnlib | 47090 | Hitachi ソリューション |
| aictracedrv_b | 47000 | AI コンサルティング |
| hhdcfltr | 46900 | Seagate テクノロジ |
| Npsvctrig | 46000 | [Microsoft] |
| klvfs | 44900 | Kaspersky ラボ |
| Klbackupflt | 44890 | Kaspersky ラボ |
| rsfxdrv .sys | 41000 | [Microsoft] |
| defilter .sys | 40900 | [Microsoft] |
| AppVVemgr | 40800 | [Microsoft] |
| wofadk. sys | 40730 | [Microsoft] |
| wof. sys | 40700 | [Microsoft] |
| fileinfo | 40500 | [Microsoft] |
| WinSetupBoot .sys | 40400 | [Microsoft] |

## <a name="span-id20000_-_29999__fsfilter_systemspanspan-id20000_-_29999__fsfilter_systemspanspan-id20000_-_29999__fsfilter_systemspan20000---29999-fsfilter-system"></a><span id="20000_-_29999__FSFilter_System"></span><span id="20000_-_29999__fsfilter_system"></span><span id="20000_-_29999__FSFILTER_SYSTEM"></span>2万-29999: FSFilter システム

なし。
