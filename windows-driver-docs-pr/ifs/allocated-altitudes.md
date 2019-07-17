---
title: 割り当て済み高度
description: 割り当て済み高度
ms.assetid: EC1993FB-5219-4C0C-A76A-05937A461C5A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b132c97b0e17b76b2b2d9d561dcc5cad6748cee9
ms.sourcegitcommit: d4ade685d5401960be55f9b44861547fbd222d35
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68246948"
---
# <a name="allocated-altitudes"></a>割り当て済み高度

フィルター マネージャー モデルを開発したファイル システム ミニフィルター ドライバーには、他のミニフィルターに対しては、ファイル システム スタックに存在する相対位置を定義する高度と呼ばれる一意の識別子が必要です。 ミニフィルターの高度はミニフィルターの要件とロード順序グループに基づいて、Microsoft によって割り当てられます。

ミニフィルターの高度の数を要求するを参照してください。[ミニフィルターの高度要求](minifilter-altitude-request.md)します。

現在の高度割り当ては、次のロード順序グループごとに以下に示します。

## <a name="span-id420000-429999filterspanspan-id420000-429999filterspanspan-id420000-429999filterspan420000---429999-filter"></a><span id="420000_-_429999__Filter"></span><span id="420000_-_429999__filter"></span><span id="420000_-_429999__FILTER"></span>420000-429999:Assert

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| ntoskrnl.exe | 425500 | マイクロソフト |
| ntoskrnl.exe | 425000 | マイクロソフト |

## <a name="span-id400000-409999fsfiltertopspanspan-id400000-409999fsfiltertopspanspan-id400000-409999fsfiltertopspan400000---409999-fsfilter-top"></a><span id="400000_-_409999__FSFilter_Top"></span><span id="400000_-_409999__fsfilter_top"></span><span id="400000_-_409999__FSFILTER_TOP"></span>400000-409999:FSFilter 上部

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| wcnfs.sys | 409900 | マイクロソフト |
| bindflt.sys | 409800 | マイクロソフト |
| cldflt.sys | 409500 | マイクロソフト |
| iorate.sys | 409010 | マイクロソフト |
| ioqos.sys | 409000 | マイクロソフト |
| fsdepends.sys | 407000 | マイクロソフト |
| sftredir.sys | 406000 | マイクロソフト |
| dfs.sys | 405000 | マイクロソフト |
| tracker.sys | 404910 | Acronis |
| csvnsflt.sys | 404900 | マイクロソフト |
| csvflt.sys | 404800 | マイクロソフト |
| Microsoft.Uev.AgentDriver.sys | 404710 | マイクロソフト |
| AppvVfs.sys | 404700 | マイクロソフト |
| CCFFilter.sys | 404600 | マイクロソフト |
| dciogrd.sys | 402010 | Datacloak 技術 |
| Dewdrv.sys | 402000 | Dell のテクノロジ |
| zsusbstorfilt.sys | 401910 | Zshield Inc |
| eaw.sys | 401900 | Raytheon サイバー ソリューション |
| TVFsfilter.sys | 401800 | TrustView |
| KKDiskProtecter.sys | 401700 | Goldmsg |
| AgentComm.sys | 401600 | Trustwave 保持 Inc |
| rvsavd.sys | 401500 | CJSC Returnil ソフトウェア |
| DGMinFlt.sys | 401410 | デジタル ガーディアン inc. |
| dgdmk.sys | 401400 | Verdasys inc. |
| tusbstorfilt.sys | 401300 | SimplyCore LLC |
| pcgenfam.sys | 401200 | Soluto |
| atrsdfw.sys | 401100 | Altiris |
| tpfilter.sys | 401000 | RedPhone セキュリティ |
| MBIG2Prot.sys | 400920 | Malwarebytes Inc |
| mbamwatchdog.sys | 400900 | Malwarebytes Corporation |
| DSESafeCtrlDrv.sys | 400803 | 上海 Eff ソフト IT |
| edevmon.sys | 400800 | ESET spol します。 s r.o. |
| vmwflstor.sys | 400700 | VMware, inc. |
| TsQBDrv.sys | 400600 | Tencent テクノロジ |
| WRAEKernel.sys | 400500 | Webroot inc. |

## <a name="span-id360000-389999fsfilteractivitymonitorspanspan-id360000-389999fsfilteractivitymonitorspanspan-id360000-389999fsfilteractivitymonitorspan360000---389999-fsfilter-activity-monitor"></a><span id="360000_-_389999__FSFilter_Activity_Monitor"></span><span id="360000_-_389999__fsfilter_activity_monitor"></span><span id="360000_-_389999__FSFILTER_ACTIVITY_MONITOR"></span>360000-389999:FSFilter 利用状況モニター

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| klboot.sys | 389510 | Kaspersky ラボ |
| klfdefsf.sys | 389500 | Kaspersky ラボ |
| CBFSFilter2017.sys | 389250 | SecureLink inc. |
| NWEDriver.sys | 389240 | Dell のテクノロジ |
| cytmon.sys | 389230 | Cytrence Inc |
| SophosED.sys | 389220 | Sophos |
| MonsterK.sys | 389210 | Somma Inc |
| IFS64.sys | 389200 | Ashampoo 開発 |
| TSTFilter.sys | 389190 | ThinScale 技術 |
| VrnsFilter.sys | 389180 | Varonis Ltd |
| lrtp.sys | 389170 | Lenovo 北京 |
| ipcomfltr.sys | 389160 | Bluzen Inc |
| SvCBT.sys | 389150 | Spharsoft テクノロジ |
| mbamshuriken.sys | 389140 | Malwarebytes |
| ContainerMonitor.sys | 389130 | 水色のセキュリティ |
| SaMFlt.sys | 389120 | DreamCrafts |
| RuiMinispy.sys | 389117 | RuiGuard Ltd |
| RuiFileAccess.sys | 389115 | RuiGuard Ltd |
| RuiEye.sys | 389113 | RuiGuard Ltd |
| RuiMachine.sys | 389111 | RuiGuard Ltd |
| windd.sys | 389110 | Comae 技術 |
| cbfsfilter2017.sys | 389105 | Basein ネットワーク |
| taobserveflt.sys | 389100 | ThinAir Labs Inc |
| vollock.sys | 389092 | Man テクノロジ Inc |
| drbdlock.sys | 389090 | Man テクノロジ Inc |
| dcfsgrd.sys | 389085 | Datacloak 技術 |
| hsmltmon.sys | 389080 | 日立ソリューション |
| AternityRegistryHook.sys | 389070 | Aternity Ltd |
| MozyNextFilter.sys | 389068 | カルボナイト Inc |
| MozyCorpFilter.sys | 389067 | カルボナイト Inc |
| MozyEntFilter.sys | 389066 | カルボナイト Inc |
| MozyOEMFilter.sys | 389065 | カルボナイト Inc |
| MozyEnterpriseFilter.sys | 389064 | カルボナイト Inc |
| MozyProFilter.sys | 389063 | カルボナイト Inc |
| MozyHomeFilter.sys | 389062 | カルボナイト Inc |
| BDSFilter.sys | 389061 | カルボナイト Inc |
| CSBFilter.sys | 389060 | カルボナイト Inc |
| ChemometecFilter.sys | 389050 | ChemoMetec |
| SentinelMonitor.sys | 389040 | SentinelOne |
| DhWatchdog.sys | 389030 | マイクロソフト |
| edrsensor.sys | 389025 | Bitdefender SRL |
| bdprivmon.sys | 389022 | Bitdefender SRL |
| NpEtw.sys | 389020 | Koby に確認 Kahane |
| OczMiniFilter.sys | 389010 | OCZ ストレージ |
| ielcp.sys | 389004 | Intel Corporation |
| IESlp.sys | 389002 | Intel Corporation |
| IntelCAS.sys | 389000 | Intel Corporation |
| boxifier.sys | 388990 | Kenubi |
| SamsungRapidFSFltr.sys | 388980 | NVELO inc. |
| drsfile.sys | 388970 | MRY inc. |
| CbFltFs4.sys | 388966 | Simopro テクノロジ |
| CrUnCopy.sys | 388964 | 深川 CloudRiver |
| aictracedrv_am.sys | 388960 | AI のコンサルティング |
| fiopolicyfilter.sys | 388954 | です inc. |
| fcontrol.sys | 388950 | SODATSW spol します。 s r.o. |
| qfilter.sys | 388940 | クォーラムのラボ |
| Redlight.sys | 388930 | Trustware Ltd |
| eps.sys | 388920 | Lumension |
| VHDTrack.sys | 388915 | Intronis Inc |
| VHDDelta.sys | 388912 | Niriva LLC |
| FSTrace.sys | 388910 | Niriva LLC |
| YahooStorage.sys | 388900 | Yahoo 日本 Corporation |
| KeWF.sys | 388890 | KEBA AG |
| epregflt.sys | 388888 | ポイントのソフトウェアを確認してください。 |
| epklib.sys | 388886 | ポイントのソフトウェアを確認してください。 |
| zsfprt.sys | 388880 | k4solution co. |
| dsflt.sys | 388876 | cEncrypt |
| bfaccess.sys | 388872 | bitFence inc. |
| xcpl.sys | 388870 | X クラウド システム |
| DCFAFilter.sys | 388866 | ManageEngine Zoho |
| RMPHVMonitor.sys | 388865 | ManageEngine Zoho |
| FAPMonitor.sys | 388864 | ManageEngine Zoho |
| EaseFlt.sys | 388860 | EaseVault Technologies inc. |
| rpwatcher.sys | 388855 | 最高レベルのセキュリティ |
| sieflt.sys | 388852 | クイック テクノロジ Pvt を回復します。 Ltd. |
| cssdlp.sys | 388851 | クイック テクノロジ Pvt を回復します。 Ltd. |
| cssdlp.sys | 388850 | CoSoSys |
| INISBDrv64.sys | 388840 | Initech inc. |
| trace.sys | 388831 | Fitsec Ltd |
| SandDriver.sys | 388830 | Fitsec Ltd |
| dskmn.sys | 388820 | Honeycomb テクノロジ |
| xkfsfd.sys | 388810 | Jiransoft co., Ltd |
| pcpifd.sys | 388800 | Jiransoft co., Ltd |
| NNTInfo.sys | 388790 | 新しいネットワーク テクノロジの限定 |
| FsMonitor.sys | 388780 | IBM |
| CVCBT.sys | 388770 | CommVault Systems, inc. |
| AwareCore.sys | 388760 | TaaSera inc. |
| laFS.sys | 388750 | NetworkProfi ltd. |
| fsnk.sys | 388740 | SoftPerfect Research |
| RGNT.sys | 388730 | HFN inc. |
| fltRs329.sys | 388720 | 世界中のセキュリティで保護された inc. |
| ospmon.sys | 388710 | SC ODEKIN ソリューション SRL |
| edsigk.sys | 388700 | エンタープライズ データ ソリューション, inc. |
| fiometer.sys | 388692 | Fusion io |
| dcSnapRestore.sys | 388690 | Fusion io |
| fam.sys | 388680 | クイック テクノロジ Pvt を回復します。 Ltd. |
| vidderfs.sys | 388675 | Vidder inc. |
| Tritiumfltr.sys | 388670 | Tritium inc. |
| HexisFSMonitor.sys | 388660 | Hexis サイバー ソリューション |
| BlackbirdFSA.sys | 388650 | BeyondTrust inc. |
| TMUMS.sys | 388642 | Trend Micro inc. |
| hfileflt.sys | 388640 | Trend Micro inc. |
| TMUMH.sys | 388630 | Trend Micro inc. |
| AcDriver.sys | 388620 | Trend Micro, inc. |
| SakFile.sys | 388610 | Trend Micro, inc. |
| SakMFile.sys | 388600 | Trend Micro, inc. |
| rsfdrv.sys | 388580 | Clonix Co |
| alcapture.sys | 388570 | エアロック デジタル Pty Ltd |
| kmNWCH.sys | 388560 | IGLOO SECURITY, inc. |
| ISIRMFmon.sys | 388550 | ALPS システム統合 CO します。 |
| EsProbe.sys | 388542 | Stormshield |
| heimdall.sys | 388540 | Arkoon ネットワーク セキュリティ |
| thetta.sys | 388532 | Syncopate |
| thetta.sys | 388531 | Syncopate |
| thetta.sys | 388530 | Syncopate |
| DTPL.sys | 388520 | SHIFT キーを押し LTD を接続します。 |
| CyOptics.sys | 388514 | Cylance inc. |
| CyProtectDrv32.sys | 388510 | Cylance inc. |
| CyProtectDrv64.sys | 388510 | Cylance inc. |
| tbfsfilt.sys | 388500 | 3 番目のリレー |
| IvAppMon.sys | 388491 | Ivanti |
| LDSecDrv.sys | 388490 | LANDESK ソフトウェア |
| SGResFlt.sys | 388480 | Samsung SDS Ltd |
| CwMem2k64.sys | 388470 | ApSoft |
| axfltdrv.sys | 388460 | Axact Pvt Ltd |
| RMDiskMon.sys | 388450 | Qingdao Ruanmei ネットワーク テクノロジ co. |
| diskactmon.sys | 388440 | Qingdao Ruanmei ネットワーク テクノロジ co. |
| Codex.sys | 388430 | GameHi co. |
| CatMF.sys | 388420 | Logichron Inc |
| RW7FsFlt.sys | 388410 | PJSC KP VTI |
| aswSP.sys | 388401 | Avast ソフトウェア |
| aswFsBlk.sys | 388400 | ALWIL Software |
| ThreatStackFIM.sys | 388380 | 脅威のスタック |
| BOsCmFlt.sys | 388370 | Barkly 保護 inc. |
| BOsFsFltr.sys | 388370 | Barkly 保護 inc. |
| FeKern.sys | 388360 | FireEye inc. |
| libwamf.sys | 388350 | Opswat, inc. |
| SZEDRDrv.sys | 388346 | SaferZone co. |
| szardrv.sys | 388345 | SaferZone co. |
| szpcmdrv.sys | 388341 | SaferZone co. |
| szdfmdrv.sys | 388340 | SaferZone co. |
| szdfmdrv_usb.sys | 388331 | SaferZone co. |
| sprtdrv.sys | 388330 | SaferZone co. |
| SWFsFltrv2.sys | 388321 | Solarwinds LLC |
| SWFsFltr.sys | 388320 | Solarwinds LLC |
| flashaccelfs.sys | 388310 | ネットワーク アプライアンス |
| changelog.sys | 388300 | ネットワーク アプライアンス |
| stcvsm.sys | 388250 | StorageCraft 技術 |
| aUpDrv.sys | 388240 | ITSTATION Inc |
| fshs.sys | 388222 | F-セキュリティで保護 |
| fshs.sys | 388221 | F-セキュリティで保護 |
| fsatp.sys | 388220 | F-セキュリティで保護 |
| SecdoDriver.sys | 388210 | Secdo |
| TGFSMF.sys | 388200 | Tetraglyph テクノロジ |
| evscase.sys | 388100 | 登場するうさぎソフトウェア Ltd 年 3 月します。 |
| VSScanner.sys | 388050 | VoodooSoft |
| HDRansomOffDrv.sys | 388044 | Heilig Defense LLC |
| HDCorrelateFDrv.sys | 388042 | Heilig Defense LLC |
| HDFileMon.sys | 388040 | Heilig Defense LLC |
| tsifilemon.sys | 388012 | インターコム inc. |
| MarSpy.sys | 388010 | インターコム inc. |
| AGSysLock.sys | 388002 | AppGuard LLC |
| AGSecLock.sys | 388001 | AppGuard LLC |
| BrnFileLock.sys | 388000 | 青のねじ山ネットワーク |
| BrnSecLock.sys | 387990 | 青のねじ山ネットワーク |
| LCmPrintMon.sys | 387978 | YATEM co. ltd. |
| LCgAdMon.sys | 387977 | YATEM co. ltd. |
| LCmAdMon.sys | 387976 | YATEM co. ltd. |
| LCgFileMon.sys | 387975 | YATEM co. ltd. |
| LCmFile.sys | 387974 | YATEM co. ltd. |
| LCgFile.sys | 387972 | YATEM co. ltd. |
| LCmFileMon.sys | 387970 | YATEM co. ltd. |
| IridiumSwitch.sys | 387960 | Confio |
| scensemon.sys | 387950 | AppiXoft |
| ruaff.sys | 387940 | RUNEXY |
| bbfilter.sys | 387930 | derivo GmbH |
| Bfmon.sys | 387920 | Baidu (香港特別行政区) の制限 |
| bdsysmon.sys | 387912 | Baidu のオンライン ネットワーク |
| BdRdFolder.sys | 387910 | Baidu (北京) |
| mlsaff.sys | 387901 | RUNEXY |
| pscff.sys | 387900 | Weing co., ltd. |
| fcnotify.sys | 387880 | TCXA ltd. |
| aaf.sys | 387860 | Actifio Inc |
| gddcv.sys | 387840 | G データ Software AG |
| wgfile.sys | 387820 | オレンジ色 WERKS Inc |
| zesfsmf.sys | 387800 | Novell |
| uamflt.sys | 387700 | Sevtechnotrans |
| ehdrv.sys | 387600 | ESET、spol します。 s r.o. |
| DattoFSF.sys | 387560 | Datto Inc |
| FileSystemCBT.sys | 387550 | Rubrik Inc |
| Snilog.sys | 387500 | Systemneeds, Inc |
| tss.sys | 387400 | Tiversa Inc |
| LmDriver.sys | 387390 | ソフト Kft します。 |
| WDCFilter.sys | 387330 | Interset inc. |
| altcbt.sys | 387320 | Altaro ltd. |
| bapfecpt.sys | 387310 | BitArmor Systems, Inc |
| bamfltr.sys | 387300 | BitArmor Systems, Inc |
| TrustedEdgeFfd.sys | 387200 | FileTek, inc. |
| MRxGoogle.sys | 387100 | Google, inc. |
| YFSDR します。SYS | 387010 | ヨコガワ研究 L Corp |
| YFSD します。SYS | 387000 | ヨコガワ研究 L Corp |
| YFSRD.sys | 386990 | ヨコガワ研究 L Corp |
| psgfoctrl.sys | 386990 | ヨコガワ研究 L Corp |
| psgdflt.sys | 386980 | ヨコガワ研究 L Corp |
| USBPDH します。SYS | 386901 | 高度なコンピューティングの開発センター |
| pecfilter.sys | 386900 | C DAC ハイデラバード |
| GKPFCB.sys | 386810 | インカ インターネット co. |
| GKPFCB64.sys | 386810 | インカ インターネット co. |
| 32 ビットの TkPcFtCb.sys | 386800 | インカ インターネット co., ltd. |
| 64 ビットで TkPcFtCb64.sys | 386800 | インカ インターネット co., ltd. |
| bmregdrv.sys | 386731 | Yandex LLC |
| bmfsdrv.sys | 386730 | Yandex LLC |
| CarbonBlackK.sys | 386720 | Bit9 inc. |
| ScAuthFSFlt.sys | 386710 | セキュリティ コード LLC |
| ScAuthIoDrv.sys | 386700 | セキュリティ コード LLC |
| mfeaskm.sys | 386610 | McAfee inc. |
| mfencfilter.sys | 386600 | McAfee |
| WinFLAHdrv.sys | 386540 | NewSoftwares&#x2024;net、inc. |
| WinFLAdrv.sys | 386530 | NewSoftwares&#x2024;net、inc. |
| WinDBdrv.sys | 386520 | NewSoftwares&#x2024;net、inc. |
| WinFLdrv.sys | 386510 | NewSoftwares&#x2024;net、inc. |
| WinFPdrv.sys | 386500 | NewSoftwares&#x2024;net、inc. |
| SkyWPDrv.sys | 386435 | 空の co., ltd. |
| SkyRGDrv.sys | 386431 | 空の co., ltd. |
| SkyAMDrv.sys | 386430 | 空の co., ltd. |
| SheedSelfProtection.sys | 386421 | SheedSoft Ltd |
| arta.sys | 386420 | SheedSoft ltd. |
| ApexSqlFilterDriver.sys | 386410 | ApexSQL LLC |
| stflt.sys | 386400 | Xacti |
| tbrdrv.sys | 386390 | クローラ グループ |
| WinTeonMiniFilter.sys | 386320 | Dmitry Stefankov |
| wiper.sys | 386310 | Dmitry Stefankov |
| DevMonMiniFilter.sys | 386300 | Dmitry Stefankov |
| VMWVvpfsd.sys | 386200 | VMware, inc. |
| RTOLogon.sys (変更) | 386200 | VMware, inc. |
| Code42Filter.sys | 386190 | Code42 |
| ConduantFSFltr.sys | 386180 | Conduant Corporation |
| KtFSFilter.sys | 386170 | Keysight テクノロジ |
| FileGuard.sys | 386140 | RES ソフトウェア |
| NetGuard.sys | 386130 | RES ソフトウェア |
| RegGuard.sys | 386120 | RES ソフトウェア |
| ImgGuard.sys | 386110 | RES ソフトウェア |
| AppGuard.sys | 386100 | RES ソフトウェア |
| RuiDiskFs.sys | 386030 | RuiGuard Ltd |
| minitrc.sys | 386020 | 保護されたネットワーク |
| cpepmon.sys | 386010 | チェックポイントのソフトウェア |
| CGWMF.sys | 386000 | NetIQ |
| ISRegFlt.sys | 385990 | Flexera Software inc. |
| ISRegFlt64.sys | 385990 | Flexera Software inc. |
| shdlpSf.sys | 385970 | Comtrue テクノロジ |
| ctrPAMon.sys | 385960 | Comtrue テクノロジ |
| shdlpMedia.sys | 385950 | Comtrue テクノロジ |
| immflex.sys | 385910 | Immidio B.V. |
| StegoProtect.sys | 385900 | Stegosystems Inc |
| brfilter.sys | 385890 | Bromium Inc |
| BrCow_x_x_x_x.sys | 385889 | Bromium Inc |
| BemK.sys | 385888 | Bromium Inc |
| secRMM.sys | 385880 | Squadra テクノロジ |
| dgfilter.sys | 385870 | DataGravity inc. |
| WFP_MRT.sys | 385860 | FireEye Inc |
| klrsps.sys | 385815 | Kaspersky ラボ |
| klsnsr.sys | 385810 | Kaspersky ラボ |
| TaniumRecorderDrv.sys | 385800 | Tanium |
| mssecflt.sys | 385600 | マイクロソフト |
| Backupreader.sys | 385500 | マイクロソフト |
| MsixPackagingToolMonitor.sys | 385410 | マイクロソフト |
| AppVMon.sys | 385400 | マイクロソフト |
| DpmFilter.sys | 385300 | マイクロソフト |
| Procmon11.sys | 385200 | マイクロソフト |
| minispy.sys - 上部 | 385100 | マイクロソフト |
| fdrtrace.sys | 385001 | マイクロソフト |
| filetrace.sys | 385000 | マイクロソフト |
| uwfreg.sys | 384910 | マイクロソフト |
| uwfs.sys | 384900 | マイクロソフト |
| locksmith.sys | 384800 | マイクロソフト |
| winload.sys | 384700 | マイクロソフト |
| SFPMonitor.sys - 上部 | 383350 | SonicWall Inc |
| FilrDriver.sys | 383340 | Micro Focus |
| rwchangedrv.sys | 383330 | Rackware |
| 飛行船 filter.sys | 383320 | AIRWare テクノロジ Ltd |
| AeFilter.sys | 383310 | Faronics Corporation |
| QQProtect.sys | 383300 | Tencent (深川) |
| QQProtectX64.sys | 383300 | Tencent (深川) |
| KernelAgent32.sys | 383260 | ZoneFox |
| WRDWIZFILEPROT します。SYS | 383251 | WardWiz |
| WRDWIZREGPROT します。SYS | 383250 | WardWiz |
| groundling32.sys | 383200 | Dell Secureworks |
| groundling64.sys | 383200 | Dell Secureworks |
| avgtpx86.sys | 383190 | AVG テクノロジ CZ |
| avgtpx64.sys | 383190 | AVG テクノロジ CZ |
| DataNow_Driver.sys | 383182 | AppSense Ltd |
| UcaFltDriver.sys | 383180 | AppSense Ltd |
| YFSD2.sys | 383170 | ヨコガワ Corpration |
| Kisknl.sys | 383160 | kingsoft |
| MWatcher.sys | 383150 | Neowiz Corporation |
| tsifilemon.sys | 383140 | インターコム inc. |
| FIM.sys | 383130 | eIQnetworks inc. |
| cFSfdrv | 383120 | Chaewool |
| ajfsprot.sys | 383110 | Analytik イエナ AG |
| isafermon | 383100 | (c)SMS |
| kfac.sys | 383000 | 北京 CA JinChen ソフトウェア co. |
| GUMHFilter.sys | 382910 | Glarysoft ltd. |
| PsAcFileAccessFilter.sys | 382902 | FUJITSU ソフトウェア |
| FJGSDis2.sys | 382900 | 富士通 |
| secure_os.sys | 382890 | FUJITSU ソーシャル サイエンス |
| ibr2fsk.sys | 382880 | FUJITSU エンジニア リング |
| FJSeparettiFilterRedirect.sys | 382860 | 富士通 |
| Fsw31rj1.sys | 382855 | 富士通 |
| da_ctl.sys | 382850 | 富士通 |
| zqFilter.sys | 382800 | magrasoft Ltd |
| ntps_fa.sys | 382700 | NTP ソフトウェア |
| sConnect.sys | 382600 | デバイスの入出力データ |
| AdaptivaClientCache32.sys | 382500 | Adaptiva |
| AdaptivaclientCache64.sys | 382500 | Adaptiva |
| phantomd.sys | 382440 | Veramine Inc |
| GoFSMF.sys | 382430 | Gorizonty Rosta Ltd |
| SWCommFltr.sys | 382420 | SnoopWall LLC |
| atflt.sys | 382410 | Atlansys ソフトウェア |
| amfd.sys | 382400 | Atlansys ソフトウェア |
| iSafeKrnl.sys | 382390 | Elex Tech Inc |
| iSafeKrnlMon.sys | 382380 | Elex Tech Inc |
| Qutmdrv.sys | 382320 | 360 のソフトウェア (北京) |
| 360box.sys | 382310 | Qihoo 360 |
| 360fsflt.sys | 382300 | 北京 Qihoo テクノロジ co. |
| scred.sys | 382210 | SoftCamp co. |
| PDGenFam.sys | 382200 | Soluto LTD |
| MCFileMon64.sys (x 64 システム) | 382100 | 三井 Electric ltd. |
| MCFileMon32.sys (x 32 のシステム) | 382100 | 三井 Electric ltd. |
| RyGuard.sys | 382050 | 深川 UNNOO 情報 Techco します。 |
| FileShareMon.sys | 382040 | 深川 UNNOO 情報 Techco します。 |
| ryfilter.sys | 382030 | 深川 UNNOO 情報 Techco します。 |
| secufile.sys | 382020 | 深川 Unnoo LTD |
| XiaobaiFs.sys | 382010 | 深川 Unnoo LTD |
| XiaobaiFsR.sys | 382000 | 深川 Unnoo LTD |
| TWBDCFilter.sys | 381910 | Trustwave |
| VPDrvNt.sys | 381900 | アンラボ |
| eetd32.sys | 381800 | Entrust Inc. |
| eetd64.sys | 381800 | Entrust Inc. |
| dnaFSMonitor.sys | 381700 | Dtex システム |
| 2000 で iwhlp2.sys | 381610 | InfoWatch |
| xp iwhlpxp.sys | 381610 | InfoWatch |
| Vista で iwhlp.sys | 381610 | InfoWatch |
| iwdmfs.sys | 381600 | InfoWatch |
| IronGateFD.sys | 381500 | rubysoft |
| MagicBackupMonitor.sys | 381400 | マジック Softworks, inc. |
| Sonar.sys | 381337 | IKARUS セキュリティ |
| ダイアログ | 381310 | Jinfengshuntai |
| MSpy.sys | 381300 | ラディスラフ Zezula |
| inuse.sys | 381200 | 登場するうさぎソフトウェア Ltd 年 3 月します。 |
| qfmon.sys | 381190 | 品質 Corporation |
| flyfs.sys | 381160 | NEC ソフト |
| serfs.sys | 381150 | NEC ソフト |
| hdrfs.sys | 381140 | NEC ソフト |
| UVMCIFSF.sys | 381130 | NEC Corporation |
| ICFClientFlt.sys | 381120 | NEC システム テクノロジ, ltd. |
| IccFileIoAd.sys | 381110 | NEC システム テクノロジ, ltd. |
| IccFilterAudit.sys | 381100 | NEC システム テクノロジ |
| IccFilterSc.sys | 381090 | InfoCage |
| Sefo.sys - 上部 | 381010 | Solusseum Inc |
| mtsvcdf.sys | 381000 | CristaLink |
| SQLsafeFilterDriver.sys | 380901 | Idera ソフトウェア |
| IderaFilterDriver.sys | 380900 | Idera |
| cbfsfilter2017.sys | 380850 | SN システム Ltd |
| xhunter1.sys | 380800 | Wellbia&#x2024;com |
| iGuard.sys | 380720 | i Guard SAS |
| cbfltfs4.sys | 380715 | Nomadesk |
| cbfltfs4.sys | 380710 | バックアップ システム Ltd |
| PkgFilter.sys | 380700 | 拡張性の高い Software inc. |
| snimg.sys | 380600 | Softnext テクノロジ |
| SK.sys | 380520 | ヒート ソフトウェア |
| mpxmon.sys | 380510 | 正のテクノロジ |
| filenamevalidator.sys | 380502 | Infotecs |
| KC3.sys | 380500 | Infotecs |
| PLPOffDrv.sys | 380492 | SK Infosec Co |
| ISFPDrv.sys | 380491 | SK Infosec Co |
| ionmonwdrv.sys | 380490 | SK Infosec Co |
| Sefo.sys - 中央 | 380480 | Solusseum Inc |
| sagntflt.sys | 380470 | ShinNihonSystec Co |
| VrExpDrv.sys | 380460 | ハウリジャパン Inc |
| srminifilterdrv.sys | 380450 | Citrix システム |
| zzpensys.sys | 380440 | Zhuan Zhuan Jing Shen |
| tedrdrv.sys | 380430 | Palo Alto Networks |
| fangcloud_autolock_driver.sys | 380420 | Hangzhou Yifangyun |
| CbSampleDrv.sys | 380020 | マイクロソフト |
| CbSampleDrv.sys | 380010 | マイクロソフト |
| CbSampleDrv.sys | 380000 | マイクロソフト |
| simrep.sys | 371100 | マイクロソフト |
| change.sys | 370160 | マイクロソフト |
| delete_flt.sys | 370150 | マイクロソフト |
| SmbResilFilter.sys | 370140 | マイクロソフト |
| usbtest.sys | 370130 | マイクロソフト |
| NameChanger.sys | 370120 | マイクロソフト |
| failMount.sys | 370110 | マイクロソフト |
| failAttach.sys | 370100 | マイクロソフト |
| stest.sys | 370090 | マイクロソフト |
| cdo.sys | 370080 | マイクロソフト |
| ctx.sys | 370070 | マイクロソフト |
| fmm.sys | 370060 | マイクロソフト |
| cancelSafe.sys | 370050 | マイクロソフト |
| message.sys | 370040 | マイクロソフト |
| passThrough.sys | 370030 | マイクロソフト |
| nullFilter.sys | 370020 | マイクロソフト |
| ntest.sys | 370010 | マイクロソフト |
| minispy.sys - 中央 | 370000 | マイクロソフト |
| isecureflt.sys | 368530 | iSecure ltd. |
| SFPMonitor.sys - 中央 | 368520 | SonicWall Inc |
| wats_se.sys | 368510 | Fujian Shen 特別行政区 |
| secure_os_mf.sys | 368500 | ハウリジャパン |
| FileMonitor.sys | 368470 | Cygna ラボ |
| asiofms.sys | 368460 | テクノロジをお勧めします。 |
| cbfsfilter2017.sys | 368450 | 絶対ソフトウェア |
| FileHubAgent.sys | 368440 | SmartFile LLC |
| nrcomgrdki.sys | 368420 | NURILAB |
| nrcomgrdka.sys | 368420 | NURILAB |
| nrpmonki.sys | 368410 | NURILAB |
| nrpmonka.sys | 368410 | NURILAB |
| nravwka.sys | 368400 | NURILAB |
| bhkavki.sys | 368390 | NURILAB |
| bhkavka.sys | 368390 | NURILAB |
| docvmonk.sys | 368380 | NURILAB |
| docvmonk64.sys | 368380 | NURILAB |
| InvProtectDrv.sys | 368370 | Invincea |
| InvProtectDrv64.sys | 368370 | Invincea |
| browserMon.sys | 368360 | Adtrustmedia |
| SfdFilter.sys | 368350 | Sandoll 通信 |
| phdcbtdrv.sys | 368340 | PHD 仮想 Tech inc. |
| sysdiag.sys | 368330 | HeroBravo テクノロジ |
| CmdCwagt.sys | 368322 | Comodo Security Solutions Inc. |
| cfrmd.sys | 368320 | Comodo Security Solutions Inc. |
| repdrv.sys | 368310 | ビジョン ソリューション |
| repmon.sys | 368300 | ビジョン ソリューション |
| cvofflineFlt32.sys | 368200 | クォンタム Corporation. |
| cvofflineFlt64.sys | 368200 | クォンタム Corporation. |
| DsDriver.sys | 368100 | Warp ディスク ソフトウェア |
| nlcbhelpx86.sys | 368000 | NetLib |
| nlcbhelpx64.sys | 368000 | NetLib |
| nlcbhelpi64.sys | 368000 | NetLib |
| wbfilter.sys | 367950 | ホワイト ボックス セキュリティ |
| LRAgentMF.sys | 367900 | LogRhythm inc. |
| Drwebfwflt.sys | 367810 | Doctor Web |
| EventMon.sys | 367800 | Doctor Web |
| dsfltfs.sys | 367760 | Digitalsense Co |
| soidriver.sys | 367750 | Sophos Plc |
| drvhookcsmf.sys | 367700 | GrammaTech, inc. |
| drvhookcsmf_amd64.sys | 367700 | GrammaTech, inc. |
| avipbb.sys | 367600 | Avira GmbH |
| FileSightMF.sys | 367500 | PA ファイルの視認 |
| csaam.sys | 367400 | Cisco Systems |
| FSMon.sys | 367300 | 1mill |
| filefilter.sys | 367100 | 北京 Zhong ハング Jiaxin コンピューター テクノロジ co., Ltd. |
| iiscache.sys | 367000 | マイクロソフト |
| nowonmf.sys | 366993 | Diskeeper Corporation |
| dktlfsmf.sys | 366992 | Diskeeper Corporation |
| DKDrv.sys | 366991 | Diskeeper Corporation |
| DKRtWrt.sys - xpsp3 署名用の一時の修正プログラム | 366990 | Diskeeper Corporation |
| HBFSFltr.sys | 366980 | Diskeeper Corporation |
| xoiv8x64.sys | 366940 | Arcserve |
| xomfcbt8x64.sys | 366930 | CA |
| KmxAgent.sys | 366920 | CA |
| KmxFile.sys | 366910 | CA |
| KmxSbx.sys | 366900 | CA |
| PointGuardVistaR32.sys | 366810 | Futuresoft |
| PointGuardVistaR64.sys | 366810 | Futuresoft |
| PointGuardVistaF.sys | 366800 | Futuresoft |
| PointGuardVista64F.sys | 366800 | Futuresoft |
| vintmfs.sys | 366789 | CondusivTechnologies |
| hiofs.sys | 366782 | Condusiv テクノロジ |
| intmfs.sys | 366781 | CondusivTechnologies |
| excfs.sys | 366780 | CondusivTechnologies |
| zampit_ml.sys | 366700 | Zampit |
| tesxnginx.sys | 366666 | Tencent テクノロジ |
| rflog.sys | 366600 | アプリケーション ストリーム, inc. |
| csmon.sys | 366582 | CyberSight Inc |
| mumdi.sys | 366540 | ZenmuTech inc. |
| LivedriveFilter.sys | 366500 | Livedrive インターネット Ltd |
| regmonex.sys | 366410 | Tranxition Corp |
| TXRegMon.sys | 366400 | Tranxition Corp |
| SDVFilter.sys | 366300 | Soliton システム株式会社 |
| eLock2FSCTLDriver.sys | 366210 | Egis Technology Inc. |
| msiodrv4.sys | 366200 | Centennial ソフトウェア Ltd |
| mmPsy32.sys | 366110 | Resplendence ソフトウェア プロジェクト |
| mmPsy64.sys | 366110 | Resplendence ソフトウェア プロジェクト |
| rrMon32.sys | 366100 | Resplendence ソフトウェア プロジェクト |
| rrMon64.sys | 366100 | Resplendence ソフトウェア プロジェクト |
| cvsflt.sys | 366000 | 登場するうさぎソフトウェア Ltd 年 3 月します。 |
| ktsyncfsflt.sys | 365920 | KnowledgeTree inc. |
| nvmon.sys | 365900 | NetVision, inc. |
| SnDacs.sys | 365810 | Informzaschita |
| SnExequota.sys | 365800 | Informzaschita |
| llfilter.sys | 365700 | SecureAxis ソフトウェア |
| hafsnk.sys | 365660 | HA Unix Pt |
| DgeDriver.sys | 365655 | Dell Software inc. |
| BWFSDrv.sys | 365650 | Quest Software inc. |
| CAADFlt.sys | 365601 | Quest Software inc. |
| QFAPFlt.sys | 365600 | Quest Software |
| XendowFLT.sys | 365570 | Credant テクノロジ |
| fmdrive.sys | 365500 | Cigital, inc. |
| EGMinFlt.sys | 365400 | WhiteCell Software inc. |
| it2reg.sys | 365315 | Soliton システム |
| it2drv.sys | 365310 | Soliton システム |
| solitkm.sys | 365300 | Soliton システム |
| pgpwdefs.sys | 365270 | Symantec |
| GEProtection.sys | 365260 | Symantec |
| diflt.sys | 365260 | Symantec corp. |
| sysMon.sys | 365250 | Symantec |
| ssrfsf.sys | 365210 | Symantec |
| emxdrv2.sys | 365200 | Symantec |
| reghook.sys | 365150 | Symantec |
| symevnt.sys | 365110 | Symantec |
| spbbcdrv.sys | 365100 | Symantec |
| bhdrvx86.sys | 365100 | Symantec |
| bhdrvx64.sys | 365100 | Symantec |
| SISIPSFileFilter | 365010 | Symantec |
| 再度 | 365000 | Symantec |
| wrpfv.sys | 364900 | マイクロソフト |
| UpGuardRealTime.sys | 364810 | UpGuard |
| usbl_ifsfltr.sys | 364800 | SecureAxis |
| ntfsf.sys | 364700 | Sun & 月上昇 |
| BssAudit.sys | 364600 | ByStorm |
| GPMiniFIlter.sys | 364500 | Kalpataru |
| AlfaFF.sys | 364400 | Alfa |
| FSAFilter.sys | 364300 | ScriptLogic |
| GcfFilter.sys | 364200 | GemacmbH |
| FFCFILT します。SYS | 364100 | FFC Limited |
| msnfsflt.sys | 364000 | マイクロソフト |
| mblmon.sys | 363900 | Packeteer |
| amsfilter.sys | 363800 | Axur について 1 秒数。 |
| rswctrl.sys | 363713 | Douzone Bizon Co |
| mcstrg.sys | 363712 | Douzone Bizon Co |
| fmkkc.sys | 363711 | Douzone Bizon Co |
| nmlhssrv01.sys | 363710 | Douzone Bizon Co |
| equ8_helper.sys | 363705 | Int3 ソフトウェア AB |
| strapvista.sys (終了バージョン) | 363700 | AvSoft テクノロジ |
| SAFE Agent.sys | 363636 | SAFE Cyberdefense |
| EstPrmon.sys | 363610 | ESTsoft corp です。 |
| Estprp.sys - 64 ビット | 363610 | ESTsoft corp です。 |
| EstRegmon.sys | 363600 | ESTsoft corp です。 |
| EstRegp.sys - 64 ビット | 363600 | ESTsoft corp です。 |
| agfsmon.sys | 363530 | TechnoKom ltd. |
| NlxFF.sys | 363520 | OnGuard システム LLC |
| Sahara.sys | 363511 | Safend |
| Santa.sys | 363510 | Safend |
| vfdrv.sys | 363500 | Viewfinity |
| topdogfsfilt.sys | 363450 | ManTech |
| xhunter64.sys | 363400 | Wellbia&#x2024;com |
| uncheater.sys | 363390 | Wellbia&#x2024;com |
| AuditFlt.sys | 363313 | Ionx ソリューション LLP |
| SPIMiniFilter.sys | 363300 | Software Pursuits inc. |
| mracdrv.sys | 363230 | メール&#x2024;Ru |
| BEDaisy.sys | 363220 | BattlEye イノベーション |
| NetAccCtrl.sys | 363200 | リンクの co します。 |
| NetAccCtrl64.sys | 363200 | リンクの co します。 |
| hpreg.sys | 363130 | HP |
| qfimdvr.sys | 363120 | Qualys inc. |
| QDocumentREF.sys | 363110 | BicDroid inc. |
| dsfemon.sys | 363100 | トポロジ Ltd |
| AmznMon.sys | 363030 | Amazon Web Services Inc |
| iothorfs.sys | 363020 | ioScience |
| ctamflt.sys | 363010 | ComTrade |
| psisolator.sys | 363000 | SharpCrafters |
| QmInspec.sys | 362990 | 北京 QiAnXin 技術。 |
| GagSecurity.sys | 362970 | 北京 Shu Yan サイエンス |
| CybKernelTracker.sys | 362960 | CyberArk ソフトウェア |
| filemon.sys | 362950 | Temasoft 株式会社 |
| SCAegis.sys | 362940 | Sogou ltd. |
| fpifp_minifilter.sys | 362930 | ForcePoint LLC です。 |
| klifks.sys | 362902 | Kaspersky ラボ |
| klifaa.sys | 362901 | Kaspersky ラボ |
| Klifsm.sys | 362900 | Kaspersky ラボ |
| nxrmflt.sys | 362860 | NextLabs |
| vast.sys | 362850 | PolyLogyx LLC |
| AALProtect.sys | 362840 | AlphaAntiLeak |
| egnfsflt.sys | 362830 | Egnyte Inc |
| RsFlt.sys | 362820 | Redstor Limited |
| CentrifyFSF.sys | 362810 | Centrify Corp |
| Sefo.sys - 下 | 362800 | Solusseum Inc |
| SFPMonitor.sys - 下 | 362700 | SonicWall Inc |
| minispy.sys - 下 | 361000 | マイクロソフト |

## <a name="span-id340000-349999fsfilterundeletespanspan-id340000-349999fsfilterundeletespanspan-id340000-349999fsfilterundeletespan340000---349999-fsfilter-undelete"></a><span id="340000_-_349999__FSFilter_Undelete"></span><span id="340000_-_349999__fsfilter_undelete"></span><span id="340000_-_349999__FSFILTER_UNDELETE"></span>340000-349999:FSFilter 削除の取り消し

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| BSSFlt.sys | 346000 | 青の靴ソフトウェア LLC |
| ThinIO.sys | 345900 | ThinScale テクノロジ |
| hmpalert.sys | 345800 | SurfRight |
| nsffkmd64.sys | 345700 | NetSTAR inc. |
| nsffkmd32.sys | 345700 | NetSTAR inc. |
| xbprocfilter.sys | 345600 | Zrxb |
| ifileguard.sys | 345500 | デバイスの入出力データ、INC. |
| undelex32.sys | 345400 | Resplendence ソフトウェア プロジェクト |
| undelex64.sys | 345400 | Resplendence ソフトウェア プロジェクト |
| starmon.sys | 345300 | Kantowitz エンジニア リング, inc. |
| mxRCycle.sys | 345200 | Avanquest |
| UdFilter.sys | 345100 | Diskeeper Corporation |
| it2prtc.sys | 345040 | Soliton システム株式会社 |
| SolRegFilter.sys | 345030 | Soliton システム株式会社 |
| SolSecBr.sys | 345020 | Soliton システム株式会社 |
| SolFCLLi.sys | 345010 | Soliton システム株式会社 |
| SolFCL.sys | 345000 | Soliton スマート秒 |
| DCVPr.sys | 340700 | SecurStar GmbH |

## <a name="span-id320000-329998fsfilteranti-virusspanspan-id320000-329998fsfilteranti-virusspanspan-id320000-329998fsfilteranti-virusspan320000---329998-fsfilter-anti-virus"></a><span id="320000_-_329998__FSFilter_Anti-Virus"></span><span id="320000_-_329998__fsfilter_anti-virus"></span><span id="320000_-_329998__FSFILTER_ANTI-VIRUS"></span>320000-329998:FSFilter ウイルス対策

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| zwPxeSvr.sys | 329330 | SecureLink inc. |
| zwASatom.sys | 329320 | SecureLink inc. |
| wscm.sys | 329310 | Fujitsu 社会科学 |
| IMFFilter.sys | 329300 | IObit 情報技術 |
| CSFlt.sys | 329290 | ConeSecurity Inc |
| ospfile_mini.sys | 329230 | OKUMA Corp |
| SoftFilterxxx.sys | 329222 | WidgetNuri Corp |
| RansomDefensexxx.sys | 329220 | WidgetNuri Corp |
| RanPodFS.sys | 329210 | Pooyan システム |
| ksfsflt.sys | 329200 | 北京 Kingsoft |
| DeepInsFS.sys | 329190 | 詳細な本能 |
| AppCheckD.sys | 329180 | CheckMAL Inc |
| spellmon.sys | 329170 | SpellSecurity |
| WhiteShield.sys | 329160 | Meidensha Corp |
| reaqtor.sys | 329150 | ReaQta ltd. |
| SE46Filter.sys | 329140 | テクノロジの Nexus AB |
| FileScan.sys | 329130 | NPcore Ltd |
| ECATDriver.sys | 329120 | EMC |
| pfkrnl.sys | 329110 | FXSEC LTD |
| epicFilter.sys | 329100 | 非表示の一眼レフ |
| b9kernel.sys | 329050 | Bit9 Inc |
| eeCtrl.sys | 329010 | Symantec |
| eraser.sys (廃止) | 329010 | Symantec |
| SRTSP.sys | 329000 | Symantec |
| SRTSPIT.sys - ia64 システム | 329000 | Symantec |
| SRTSP64 します。SYS x64 システム | 329000 | Symantec |
| a2ertpx86.sys | 328920 | Emsi ソフトウェア GmbH |
| a2ertpx64.sys | 328920 | Emsi ソフトウェア GmbH |
| a2gffx86.sys - x86 | 328910 | Emsi ソフトウェア GmbH |
| a2gffx64.sys - x64 | 328910 | Emsi ソフトウェア GmbH |
| a2gffi64.sys - IA64 | 328910 | Emsi ソフトウェア GmbH |
| a2acc.sys | 328900 | Emsi ソフトウェア GmbH |
| x64 a2acc64.sys システム | 328900 | Emsi ソフトウェア GmbH |
| FlightRecorder.sys | 328850 | Malwarebytes corp. |
| si32_file.sys | 328810 | Scargo Inc |
| si64_file.sys | 328810 | Scargo Inc |
| mbam.sys | 328800 | Malwarebytes corp. |
| EnigmaFileMonDriver.sys | 328770 | EnigmaSoft |
| KUBWKSP.sys | 328750 | Netlor SAS |
| hcp_kernel_acq.sys | 328740 | refractionPOINT |
| SegiraFlt.sys | 328730 | Segira LLC |
| wdocsafe.sys | 328722 | Cheetah Mobile inc. |
| lbprotect.sys | 328720 | Cheetah Mobile inc. |
| eamonm.sys | 328700 | ESET、spol します。 s r.o. |
| klam.sys | 328650 | Kaspersky ラボ |
| MaxProc64.sys | 328620 | 最大の安全なソフトウェア |
| MaxProtector.sys | 328610 | 最大の安全なソフトウェア |
| maxcryptmon.sys | 328601 | 最大の安全なソフトウェア |
| SDActMon.sys | 328600 | 最大の安全なソフトウェア |
| fileflt.sys | 328540 | Trend Micro inc. |
| TmEsFlt.sys | 328530 | Trend Micro inc. |
| TmEyes.sys | 328520 | Trend Micro inc. |
| tmevtmgr.sys | 328510 | Trend Micro inc. |
| tmpreflt.sys | 328500 | 傾向 |
| vcMFilter.sys | 328400 | SGRI co., ltd. |
| SAFsFilter.sys | 328300 | 光速 Systems inc. |
| vsepflt.sys | 328200 | VMware, inc. |
| VFileFilter.sys(renamed) | 328200 | VMware, inc. |
| sfavflt.sys | 328130 | Sangfor テクノロジ |
| sfavflt.sys | 328120 | Sangfor テクノロジ |
| drivesentryfilterdriver2lite.sys | 328100 | DriveSentry Inc |
| WdFilter.sys | 328010 | マイクロソフト |
| mpFilter.sys | 328000 | マイクロソフト |
| vrSDetri.sys | 327801 | ETRI |
| vrSDetrix.sys | 327800 | ETRI |
| AhkSvPro.sys | 327720 | Ahkun co. |
| AhkUsbFW.sys | 327710 | Ahkun co. |
| AhkAMFlt.sys | 327700 | Ahkun co. |
| PSINPROC します。SYS | 327620 | パンダ セキュリティ |
| PSINFILE します。SYS | 327610 | パンダ セキュリティ |
| amfsm.sys - Windows XP/2003 の x64 | 327600 | パンダ セキュリティ |
| amm8660.sys - Windows Vista x86 | 327600 | パンダ セキュリティ |
| amm6460.sys - Windows Vista x64 | 327600 | パンダ セキュリティ |
| ADSpiderDoc.sys | 327550 | Digitalonnet |
| BkavAutoFlt.sys | 327542 | Bkav Corporation |
| BkavSdFlt.sys | 327540 | Bkav Corporation |
| easyanticheat.sys | 327530 | EasyAntiCheat ソリューション |
| 5nine.cbt.sys | 327520 | 5 nine Software inc. |
| caavFltr.sys | 327510 | コンピューター Assoc |
| ino_fltr.sys | 327500 | コンピューター Assoc |
| SECOne_USB.sys | 327426 | GRGBanking 機器 |
| SECOne_Proc10.sys | 327424 | GRGBanking 機器 |
| SECOne_REG10.sys | 327422 | GRGBanking 機器 |
| SECOne_FileMon10.sys | 327420 | GRGBanking 機器 |
| WCSDriver.sys | 327410 | 白のクラウド セキュリティ |
| 360qpesv.sys | 327404 | 360 のソフトウェア (北京) |
| dsark.sys | 327402 | Qihoo 360 |
| 360avflt.sys | 327400 | Qihoo 360 |
| scifsflt.sys | 327333 | SECUI Corporation |
| ANVfsm.sys | 327310 | Arcdo |
| CDrRSFlt.sys | 327300 | Arcdo |
| mfdriver.sys | 327250 | Imperva inc. |
| EPSMn.sys | 327200 | SGA |
| VTSysFlt.sys | 327150 | 北京 Venus |
| TesMon.sys | 327130 | Tencent |
| QQSysMonX64.sys | 327125 | Tencent |
| QQSysMon.sys | 327120 | Tencent |
| TSysCare.sys | 327110 | 深川 Tencent コンピューター システムの会社の制限 |
| TFsFlt.sys | 327100 | 深川 Tencent コンピューター システムの会社の制限 |
| avmf.sys | 327000 | Authentium |
| BDFileDefend.sys | 326916 | Baidu (北京) |
| BDsdKit.sys | 326914 | Baidu オンライン ネットワーク テクノロジ (北京) co. |
| bd0003.sys | 326912 | Baidu オンライン ネットワーク テクノロジ (北京) co. |
| Bfilter.sys | 326910 | Baidu (香港特別行政区) の制限 |
| NeoKerbyFilter | 326900 | NeoAutus |
| egnfsflt.sys | 326830 | Egnyte Inc |
| RsFlt.sys | 326820 | Redstor Limited |
| trpmnflt.sys | 326810 | TRAPMINE A.S. |
| PLGFltr.sys | 326800 | Paretologic |
| WrdWizSecure64.sys | 326730 | WardWiz |
| wrdwizscanner.sys | 326720 | WardWiz |
| AshAvScan.sys | 326700 | Ashampoo GmbH & Co. KG |
| Zyfm.sys | 326666 | ZhengYong InfoTech ltd. |
| csaav.sys | 326600 | Cisco Systems |
| oavfm.sys | 326550 | HSM の IT サービス Gmbh |
| SegMD.sys | 326520 | Segurmatica |
| SegMP.sys | 326510 | Segurmatica |
| SegF.sys | 326500 | Segurmatica |
| eeyehv.sys | 326400 | eEye デジタル セキュリティ |
| eeyehv64.sys | 326400 | eEye デジタル セキュリティ |
| CpAvFilter.sys | 326311 | CodeProof テクノロジ Inc |
| CpAvKernel.sys | 326310 | CodeProof テクノロジ Inc |
| NovaShield.sys | 326300 | Securitas Technologies, Inc. |
| SheedAntivirusFilterDriver.sys | 326290 | SheedSoft Ltd |
| bSyirmf.sys | 326260 | BLACKFORT セキュリティ |
| bSysp.sys | 326250 | BLACKFORT セキュリティ |
| bSymfdm.sys | 326240 | BLACKFORT セキュリティ |
| bSywl.sys | 326235 | BLACKFORT セキュリティ |
| bSyrtm.sys | 326230 | BLACKFORT セキュリティ |
| bSyaed.sys | 326220 | BLACKFORT セキュリティ |
| bSyar.sys | 326210 | BLACKFORT セキュリティ |
| BdFileSpy.sys | 326200 | インストーラー |
| npxgd.sys | 326160 | インカ インターネット co. |
| npxgd64.sys | 326160 | インカ インターネット co. |
| tkpl2k.sys | 326150 | インカ インターネット co. |
| tkpl2k64.sys | 326150 | インカ インターネット co. |
| GKFF.sys | 326140 | インカ インターネット co. |
| GKFF64.sys | 326140 | インカ インターネット co. |
| tkdac2k.sys | 326130 | インカ インターネット co. |
| tkdacxp.sys | 326130 | インカ インターネット co. |
| tkdacxp64.sys | 326130 | インカ インターネット co. |
| tksp2k.sys | 326120 | インカ インターネット co. |
| tkspxp.sys | 326120 | インカ インターネット co. |
| tkspxp64.sys | 326120 | インカ インターネット co. |
| tkfsft.sys | 326110 | インカ インターネット co., Ltd |
| tkfsft64.sys - 64 ビット | 326110 | インカ インターネット co., Ltd |
| tkfsavxp.sys - 32 ビット | 326100 | インカ インターネット co., Ltd |
| tkfsavxp64.sys - 64 ビット | 326100 | インカ インターネット co., Ltd |
| SMDrvNt.sys | 326040 | アンラボ |
| ATamptNt.sys | 326030 | アンラボ |
| V3Flt2k.sys | 326020 | アンラボ |
| V3MifiNt.sys | 326010 | Ahnlab |
| V3Ift2k.sys | 326000 | Ahnlab |
| V3IftmNt.sys (古い名前) | 326000 | Ahnlab |
| ArfMonNt.sys | 325990 | Ahnlab |
| AhnRghLh.sys | 325980 | Ahnlab |
| AszFltNt.sys | 325970 | Ahnlab |
| OMFltLh.sys | 325960 | Ahnlab |
| V3Flu2k.sys | 325950 | Ahnlab |
| TfFregNt.sys | 325940 | AhnLab inc. |
| AdcVcsNT.sys | 325930 | Ahnlab |
| vcdriv.sys | 325820 | Greatsoft Corp.Ltd |
| vcreg.sys | 325810 | Greatsoft Corp.Ltd |
| vchle.sys | 325800 | Greatsoft Corp.Ltd |
| NxFsMon.sys | 325700 | Novatix Corporation |
| AntiLeakFilter.sys | 325600 | 個々 の開発者 (Soft3304) |
| NanoAVMF.sys | 325510 | パンダ ソフトウェア |
| shldflt.sys | 325500 | パンダ ソフトウェア |
| nprosec.sys | 325410 | Norman ASA |
| nregsec.sys | 325400 | Norman ASA |
| issregistry.sys | 325300 | IBM |
| THFilter.sys | 325200 | Sybonic システム Inc |
| pervac.sys | 325100 | PerSystems SA |
| avgmfx86.sys | 325000 | AVG さら |
| avgmfx64.sys | 325000 | AVG さら |
| avgmfi64.sys | 325000 | AVG さら |
| avgmfrs.sys (終了バージョン) | 325000 | AVG さら |
| FortiAptFilter.sys | 324930 | Fortinet inc. |
| fortimon2.sys | 324920 | Fortinet inc. |
| fortirmon.sys | 324910 | Fortinet inc. |
| fortishield.sys | 324900 | Fortinet inc. |
| mscan rt.sys | 324800 | SecureBrain Corporation |
| sysdiag.sys | 324600 | Huorong セキュリティ |
| agentrtm64.sys | 324510 | WINS CO します。 LTD |
| rswmon.sys | 324500 | WINS CO します。 LTD |
| mwfsmfltr.sys | 324420 | MicroWorld ソフトウェア サービス Pvt. Ltd. |
| gtkdrv.sys | 324410 | GridinSoft LLC |
| GbpKm.sys | 324400 | ガス Tecnologia |
| crnsysm.sys | 324310 | Coranti inc. |
| crncache32.sys | 324300 | Coranti inc. |
| crncache64.sys | 324300 | Coranti inc. |
| egambit.sys | 324242 | TEHTRI セキュリティ |
| drwebfwft.sys | 324210 | Doctor Web |
| DwShield.sys | 324200 | Doctor Web |
| DwShield64.sys | 324200 | Doctor Web |
| IProtect.sys | 324150 | EveryZone inc. |
| TvFiltr.sys | 324140 | EveryZone inc. |
| TvDriver.sys | 324130 | EveryZone inc. |
| TvSPFltr.sys | 324120 | EveryZone inc. |
| TvPtFile.sys | 324110 | EveryZone inc. |
| TvMFltr.sys | 324100 | Everyzone |
| SophosED.sys | 324050 | Sophos |
| SAVOnAccess.sys | 324010 | Sophos |
| savonaccess.sys | 324000 | Sophos |
| sld.sys | 323990 | Sophos |
| OADevice.sys | 323900 | 高さこと |
| pwipf6.sys | 323800 | PWI, inc. |
| EstRkmon.sys | 323700 | ESTsoft corp です。 |
| EstRkr.sys - 64 ビット | 323700 | ESTsoft corp です。 |
| dwprot.sys | 323610 | Doctor Web |
| Spiderg3.sys | 323600 | Doctor Web ltd. |
| STKrnl64.sys | 323500 | Verdasys Inc |
| UFDFilter.sys | 323400 | Yoggie |
| SCFltr.sys | 323300 | SecurityCoverage, inc. |
| fildds.sys | 323200 | Filseclab |
| fsfilter.sys | 323100 | MastedCode Ltd |
| fpav_rtp.sys | 323000 | f で保護します。 |
| cwdriver.sys | 322900 | Leith Bade |
| AYFilter.sys | 322810 | ESTsoft |
| Rtw.sys | 322800 | ESTsoft |
| RSRtw.sys | 322790 | ESTsecurity Corp |
| RSPCRtw.sys | 322780 | ESTsecurity Corp |
| HookSys.sys | 322700 | 北京増大情報 Technology Corporation Limited |
| snscore.sys | 322600 | S.N.Safe & ソフトウェア |
| ssvhook.sys | 322500 | SecuLution GmbH |
| strapvista.sys | 322400 | AvSoft テクノロジ |
| strapvista64.sys | 322400 | AvSoft テクノロジ |
| sascan.sys | 322300 | SecureAge テクノロジ |
| savant.sys | 322200 | 教養保護, inc. |
| VrARnFlt.sys | 322161 | ハウリジャパン |
| VrBBDFlt.sys | 322160 | ハウリジャパン |
| vrSDfmx.sys | 322153 | ハウリジャパン |
| vrSDfmx.sys | 322152 | ハウリジャパン |
| vrSDam.sys | 322151 | ハウリジャパン |
| vrSDam.sys | 322150 | ハウリジャパン |
| VRAPTFLT.sys | 322140 | ハウリジャパン inc. |
| VrAptDef.sys | 322130 | ハウリジャパン |
| VrSdCore.sys | 322120 | ハウリジャパン |
| VrFsFtM.sys | 322110 | ハウリジャパン |
| VrFsFtMX.sys(AMD64) | 322110 | ハウリジャパン |
| vradfil2.sys | 322100 | ハウリジャパン |
| fsgk.sys | 322000 | f-セキュリティで保護 |
| bouncer.sys | 321950 | CoreTrace 社 |
| PCTCore64.sys | 321910 | PC ツール擬似 Ltd. |
| PCTCore.sys (古い名前) | 321910 | PC ツール擬似 Ltd. |
| ikfilesec.sys | 321900 | PC ツール擬似 Ltd. |
| ZxFsFilt.sys | 321800 | オーストラリアのプロジェクト |
| antispyfilter.sys | 321700 | C NetMedia Inc |
| PZDrvXP.sys | 321600 | VisionPower co., ltd. |
| ggc.sys | 321510 | クイック TechnologiesPvt を回復します。 Ltd. |
| catflt.sys | 321500 | クイック TechnologiesPvt を回復します。 Ltd. |
| bdsflt.sys | 321490 | クイック テクノロジ Pvt を回復します。 Ltd. |
| arwflt.sys | 321480 | クイック テクノロジ Pvt を回復します。 Ltd. |
| csagent.sys | 321410 | CrowdStrike ltd. |
| kmkuflt.sys | 321400 | Komoku inc. |
| ntguard.sys | 321337 | IKARUS セキュリティ |
| epdrv.sys | 321320 | McAfee inc. |
| mfencoas.sys | 321310 | McAfee inc. |
| mfehidk.sys | 321300 | McAfee inc. |
| swin.sys | 321250 | McAfee inc. |
| CyvrFsfd.sys | 321234 | Palo Alto Networks |
| cmdccav.sys | 321210 | Comodo グループ inc. |
| cmdguard.sys | 321200 | Comodo グループ inc. |
| K7Sentry.sys | 321100 | K7 プライベート Ltd. のコンピューティング |
| nsminflt.sys | 321050 | NHN |
| nsminflt64.sys | 321050 | NHN |
| nvcmflt.sys | 321000 | Norman |
| dgsafe.sys | 320950 | KINGSOFT |
| issfltr.sys | 320900 | ISS |
| hbflt.sys | 320840 | BitDefender SRL |
| bdsvm.sys | 320830 | Bitdefender |
| gzflt.sys | 320820 | BitDefender SRL |
| bddevflt.sys | 320812 | BitDefender SRL |
| ignis.sys | 320811 | BitDefender SRL |
| AVCKF します。SYS | 320810 | BitDefender SRL |
| bdfsfltr.sys | 320800 | Softwin |
| bdfm.sys | 320790 | Softwin |
| gemma.sys | 320782 | BitDefender SRL |
| Atc.sys | 320781 | BitDefender SRL |
| AVC3 します。SYS | 320780 | BitDefender SRL |
| TRUFOS します。SYS | 320770 | BitDefender SRL |
| aswmonflt.sys | 320700 | Alwil |
| HookCentre.sys | 320602 | G データ |
| PktIcpt.sys | 320601 | G データ |
| MiniIcpt.sys | 320600 | G データ |
| avgntflt.sys | 320500 | Avira GmbH |
| klam.sys | 320450 | Kaspersky ラボ |
| klbg.sys | 320440 | Kaspersky |
| kldback.sys | 320430 | Kaspersky |
| kldlinf.sys | 320420 | Kaspersky |
| kldtool.sys | 320410 | Kaspersky |
| klif.sys | 320401 | Kaspersky ラボ |
| klif.sys | 320400 | Kaspersky |
| klam.sys | 320350 | Kaspersky ラボ |
| hsmltwhl.sys | 320340 | 日立ソリューション |
| hssfwhl.sys | 320330 | 日立ソリューション |
| DeepInsFS.sys | 320320 | ディープ本能 ltd. |
| avfsmn.sys | 320310 | Anvisoft |
| lbd.sys | 320300 | Lavasoft AB |
| pavdrv.sys | 320210 | Panzor サイバー セキュリティ |
| rvsmon.sys | 320200 | CJSC Returnil ソフトウェア |
| WRKrn.sys | 320110 | Webroot inc. |
| ssfmonm.sys | 320100 | Webroot ソフトウェア, inc. |
| vk_fsf.sys | 320050 | AxBx |
| VirtualAgent.sys | 320005 | Symantec |

## <a name="span-id300000-309998fsfilterreplicationspanspan-id300000-309998fsfilterreplicationspanspan-id300000-309998fsfilterreplicationspan300000---309998-fsfilter-replication"></a><span id="300000_-_309998__FSFilter_Replication"></span><span id="300000_-_309998__fsfilter_replication"></span><span id="300000_-_309998__FSFILTER_REPLICATION"></span>300000-309998:FSFilter レプリケーション

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| IntelCAS.sys | 309100 | Intel Corporation |
| mvfs.sys | 309000 | IBM Corporation |
| frxccd.sys | 306000 | FSLogix inc. |
| fsrecord.sys | 305000 | マイクロソフト |
| InstMon.sys | 304201 | Numecent inc. |
| StreamingFSD.sys | 304200 | Numecent inc. |
| ubcminifilterdriver.sys | 304100 | Ullmore ltd. |
| replistor.sys | 304000 | Legato |
| stfsd.sys | 303900 | 祈りテクノロジ |
| xomf.sys | 303800 | CA (XOSOFT) |
| nfid.sys | 303700 | グループ Ltd の採用 |
| sybfilter.sys | 303600 | Sybase, inc. |
| rfsfilter.sys | 303500 | Evidian |
| cvmfsj.sys | 303400 | CommVault Systems, inc. |
| iOraFilter.sys | 303300 | Infonic plc |
| bkbmfd32.sys (x86) | 303200 | BakBone ソフトウェア, Inc |
| bkbmfd64.sys (x64) | 303200 | BakBone ソフトウェア, Inc |
| mblvn.sys | 303100 | Packeteer |
| AV12NFNT.sys | 303000 | AhnLab |
| mDP_win_mini.sys | 302900 | マクロの影響 |
| ctxubs.sys | 302800 | Citrix Systems inc. |
| rrepfsf.sys | 番号 302700 | Rose データ システム Inc |
| cbfsfilter2017.sys | 301900 | 非常に柔軟なソフトウェア |
| AxFilter.sys | 301800 | Axcient inc. |
| vxfsrep.sys | 301700 | Symantec |
| dellcapfd.sys | 301600 | Dell Inc. |
| Sptres.sys | 301500 | Safend |
| OfficeBackup.sys | 301400 | Ushus テクノロジ |
| pcvnfilt.sys | 301300 | Blue Coat |
| repdac.sys | 301200 | NSI |
| repkap.sys | 301100 | NSI |
| repdrv.sys | 301000 | NSI |

## <a name="span-id280000-289998fsfiltercontinuousbackupspanspan-id280000-289998fsfiltercontinuousbackupspanspan-id280000-289998fsfiltercontinuousbackupspan280000---289998-fsfilter-continuous-backup"></a><span id="280000_-_289998__FSFilter_Continuous_Backup"></span><span id="280000_-_289998__fsfilter_continuous_backup"></span><span id="280000_-_289998__FSFILTER_CONTINUOUS_BACKUP"></span>280000-289998:FSFilter 継続的なバックアップ

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| Klcdp.sys | 288900 | Kaspersky ラボ |
| splitinfmon.sys | 288800 | 無限大を分割します。 |
| versamatic.sys | 288700 | Acertant 技術 |
| Yfilemon.sys | 288690 | Yarisoft |
| ibac.sys | 288600 | Idealstor、LLC です。 |
| fkdriver.sys | 288500 | Filekeeper |
| AAFileFilter.sys | 288300 | Dell Inc. |
| hyperoo.sys | 288400 | Hyperoo Ltd |
| HyperBacCA.sys | 285000 | Red Gate ソフトウェア Ltd |
| ZMSFsFltr.sys | 284400 | 点 InfoTech |
| AlfaSC.sys | 284300 | Alfa Corporation |
| hie_ifs.sys | 284200 | Hie Electronics, inc. |
| AAFs.sys | 284100 | AppAssure ソフトウェア |
| defilter.sys (旧) | 284000 | マイクロソフト |
| aFsvDrv.sys | 283100 | ITSTATION Inc |
| tilana.sys | 283000 | Tilana Sys |
| VmDPFilter.sys | 282900 | マクロの影響 |
| LbFilter.sys | 281700 | Linkverse 株式会社 |
| fbsfd.sys | 281600 | Ferro ソフトウェア |
| dupleemf.sys | 281500 | Duplee SPI、S.L. |
| file_tracker.sys | 281420 | Acronis inc. |
| exbackup.sys | 281410 | Acronis inc. |
| afcdp.sys | 281400 | Acronis inc. |
| dcefltr.sys | 281300 | Cofio ソフトウェア Ltd |
| ipmrsync_mfilter.sys | 281200 | OpenMars 企業 |
| cascade.sys | 281100 | JP ソフトウェア |
| filearchive.sys | 281000 | コードのエラー発生 |
| syscdp.sys | 280900 | [Ok] をシステム AB |
| dpnedriver.sys (x86) | 280850 | HP |
| dpnedriver64.sys (x64) | 280850 | HP |
| hpchgflt.sys | 280800 | HP |
| VirtFile.sys | 280700 | Symantec |
| DeqoCPS.sys | 280600 | Deqo |
| LV_Tracker.sys | 280500 | LiveVault |
| cpbak.sys | 280410 | チェックポイントのソフトウェア |
| tdmonxp.sys | 280400 | TimeData |
| nvfr_cpd | 280310 | Bakbone Software inc. |
| nvfr_fdd | 280300 | Bakbone Software inc. |
| Sptbkp.sys | 280290 | Safend |
| accessmonitor.sys | 280280 | Briljant Ekonomisystem |

## <a name="span-id260000-269998fsfiltercontentscreenerspanspan-id260000-269998fsfiltercontentscreenerspanspan-id260000-269998fsfiltercontentscreenerspan260000---269998-fsfilter-content-screener"></a><span id="260000_-_269998__FSFilter_Content_Screener"></span><span id="260000_-_269998__fsfilter_content_screener"></span><span id="260000_-_269998__FSFILTER_CONTENT_SCREENER"></span>260000-269998:FSFilter コンテンツこだわりの検索

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| Klshadow.sys | 268300 | Kaspersky ラボ |
| TN28.sys | 268290 | ID の認証の技術 |
| PGDriver.sys | 268280 | Avecto Ltd |
| itseczvdb.sys | 268270 | Innotium Inc |
| isarsd.sys | 268260 | ISARS |
| zeoscanner.sys | 268255 | PCKeeper |
| fileHiders.sys | 268250 | PCKeeper |
| cbfltfs4 ObserveIT.sys | 268240 | ObserveIT |
| hipara.sys | 268230 | Allsum LLC |
| AliFileMonitorDriver.sys | 268220 | Alibaba |
| writeGuard.sys | 268210 | TCXA ltd. |
| KKUDKProtectKer.sys | 268200 | Goldmessage テクノロジ co します。 |
| HAWKFIMInt.sys | 268190 | HAWK ネットワーク防御 |
| esaccctl.sys | 268180 | EgoSecure GmbH |
| WSguard.sys | 268170 | ワイパー ソフトウェア |
| Atomizer.sys | 268160 | DragonFlyCodeWorks |
| farwflt.sys | 268150 | Malwarebytes |
| ADSpiderEx2.sys | 268140 | Digitalonnet |
| sdfilter.sys | 268130 | Igor Zorkov |
| Safe.sys | 268120 | rian@alum.mit.edu |
| mydlpdelete scanner.sys | 268110 | Medra Teknoloji |
| mydlpscanner.sys | 268100 | Medra Teknoloji |
| hnpro.sys | 268040 | Solupia |
| DLDriverNetMini.sys | 268030 | DeviceLock Inc |
| ENFFLTDRV.sys | 268020 | Enforcive システム |
| imagentpg.sys | 268012 | Infomaximum |
| crocopg.sys | 268010 | Infomaximum |
| sbapifs.sys | 268000 | Sunbelt ソフトウェア |
| H6kernNT.sys | 267920 | H6N テクノロジ LLC |
| SGKD32 します。SYS | 267910 | NetSection セキュリティ |
| IccFilter.sys | 267900 | NEC システム テクノロジ |
| tflbc.sys | 267800 | Tani Electronics Corporation |
| ArmFlt.sys | 267000 | 防御のウイルス対策 |
| WBDrv.sys | 266700 | Axiana LLC |
| DMSamFilter.sys | 266600 | Digimarc corp. |
| mumbl.sys | 266540 | ZenmuTech inc. |
| 5nine.cbt.sys | 266100 | 5 nine Software inc. |
| bsfs.sys | 266000 | クイック TechnologiesPvt を回復します。 Ltd.  |
| XXRegSFilter.sys | 265910 | Zhe Jiang Xinxin ソフトウェア技術です。 |
| XXSFilter.sys | 265900 | Zhe Jiang Xinxin ソフトウェア技術です。 |
| AloahaUSBBlocker.sys | 265800 | Wrocklage Intermedia |
| frxdrv.sys | 265700 | FSLogix inc. |
| FolderSecure.sys | 265600 | 最大の安全なソフトウェア |
| XendowFLTC.sys | 265570 | Credant テクノロジ |
| RepDac | 265500 | ビジョン ソリューション |
| tbbdriver.sys | 265400 | Tedesi |
| spcgrd.sys | 265300 | FUJITSU 広範なソリューション |
| fdtlock.sys | 265250 | FUJITSU 広範なソリューションとコンサルティング inc. |
| ssfFSC.sys | 265200 | SECUWARE S.L. |
| GagSecurity.sys | 265120 | 北京 Shu Yan サイエンス |
| PrintDriver.sys | 265110 | 北京 Shu Yan サイエンス |
| activ.sys | 265100 | Rapidware Pty Ltd |
| avscan.sys | 265010 | マイクロソフト |
| scanner.sys | 265000 | マイクロソフト |
| DI_fs.sys | 264910 | ソフト SB |
| wgnpos.sys | 264900 | Orchestria |
| odfltr.sys | 264810 | テクノロジのします。 |
| ncpafltr.sys | 264800 | テクノロジのします。 |
| ct.sys | 264700 | Haute をセキュリティで保護 |
| fvefsmf.sys | 264600 | Fortisphere, inc. |
| block.sys | 264500 | 自律性 Systems Limited |
| csascr.sys | 264400 | Cisco Systems |
| SymAFR.sys | 264300 | Symantec |
| cwnep.sys | 264200 | Websense inc. |
| spywareremover.sys | 264150 | C Netmedia |
| malwarebot.sys | 264140 | C Netmedia |
| antispywarebot.sys | 264130 | 2Squared inc. |
| adwarebot.sys | 264120 | スパイウェア対策 LLC |
| antispyware.sys | 264110 | スパイウェア対策 LLC |
| spywarebot.sys | 264100 | C Netmedia |
| nomp3.sys | 264000 | Hamish Speirs (プライベート開発者向け) |
| dlfilter.sys | 263900 | ソフトウェアのスター フィールド |
| sifsp.sys | 263800 | Secure Islands Technologies LTD |
| DLFsFlt.sys | 263700 | CenterTools ソフトウェア GmbH |
| SamKeng.sys | 263600 | Syvik Co, ltd. |
| rml.sys | 263500 | Logis IT Gmbh サービス |
| vfsmfd.sys | 263410 | Vontu inc. |
| vfsmfd.sys | 263400 | Vontu inc. |
| acfilter.sys | 263300 | Avalere, inc. |
| psecfilter.sys | 263200 | MDI 実験, inc. |
| SolRedirect.sys | 263110 | Soliton システム |
| solitkm.sys | 263100 | Soliton システム |
| ipcfs.sys | 263000 | NetVeda |
| netgateav_access.sys | 262910 | NETGATE 技術。 s.r.o. |
| spyemrg_access.sys | 262900 | NETGATE 技術。 s.r.o. |
| pxrmcet.sys | 262800 | Proxure inc. |
| EgisTecFF.sys | 262700 | Egis Technology Inc. |
| fgcpac.sys | 262600 | Fortres Grand corp. |
| saappctl.sys | 262510 | SecureAge テクノロジ |
| sadlp.sys | 262500 | SecureAge テクノロジ |
| CRExecPrev.sys | 262410 | Cybereason |
| PEG2.sys | 262400 | PE GUARD |
| AdminRunFlt.sys | 262300 | Simon ジャービス |
| wvscr.sys | 262200 | ハートフォード, コネチカット州 Wei Tech inc. |
| psepfilter.sys | 262100 | 絶対ソフトウェア |
| SAMDriver.sys | 262000 | Summit IT |
| emrcore.sys | 261920 | Ivanti Inc |
| wire_fsfilter.sys | 261910 | ThreatSpike ラボ |
| AMFileSystemFilter.sys | 261900 | AppSense Ltd |
| mtflt.sys | 261880 | mTalos inc. |
| nxrmflt.sys | 261680 | NextLabs, inc. |
| oc_fsfilter.sys | 261300 | Aval Raiffeisen 銀行 |
| hdlpflt.sys | 261200 | McAfee inc. |
| CCFFilter.sys | 261160 | マイクロソフト |
| cbafilt.sys | 261150 | マイクロソフト |
| SmbBandwidthLimitFilter.sys | 261110 | マイクロソフト |
| DfsrRo.sys | 261100 | マイクロソフト |
| DataScrn.sys | 261000 | マイクロソフト |
| ldusbro.sys | 260900 | LANDesk inc. |
| FileScreenFilter.sys | 260800 | Veritas |
| cpAcOnPnP.sys | 260720 | conpal GmbH |
| cpsgfsmf.sys | 260710 | conpal GmbH |
| psmmfilter.sys | 260700 | PolyServe |
| pctefa.sys | 260650 | PC ツール擬似 Ltd. |
| pctefa64.sys | 260650 | PC ツール擬似 Ltd. |
| symefasi.sys | 260610 | Symantec |
| symefa.sys | 260600 | Symantec |
| symefa64.sys | 260600 | Symantec |
| aictracedrv_cs.sys | 260500 | AI のコンサルティング |
| DWFIxxxx.sys | 260410 | SciencePark Corporation |
| DWFIxxxx.sys | 260400 | SciencePark Corporation |
| DSDriver.sys | 260330 | ManageEngine Zoho Corp |
| mcfltlab.sys | 260320 | 北京 MicroColor |
| FDriver.sys | 260310 | Fox IT |
| iqpk.sys | 260300 | Secure Islands Technologies LTD |
| VHDFlt.sys | 260240 | Dell |
| VHDFlt.sys | 260230 | Dell |
| VHDFlt.sys | 260220 | Dell |
| VHDFlt.sys | 260210 | Dell |

## <a name="span-id240000-249999fsfilterquotamanagementspanspan-id240000-249999fsfilterquotamanagementspanspan-id240000-249999fsfilterquotamanagementspan240000---249999-fsfilter-quota-management"></a><span id="240000_-_249999__FSFilter_Quota_Management"></span><span id="240000_-_249999__fsfilter_quota_management"></span><span id="240000_-_249999__FSFILTER_QUOTA_MANAGEMENT"></span>240000-249999:FSFilter クォータの管理

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| ntps_qfs.sys | 245100 | NTP ソフトウェア |
| PSSFsFilter.sys | 245000 | PSS システム |
| Sptqmg.sys | 245300 | Safend |
| storqosflt.sys | 244000 | マイクロソフト |

## <a name="span-id220000-229999fsfiltersystemrecoveryspanspan-id220000-229999fsfiltersystemrecoveryspanspan-id220000-229999fsfiltersystemrecoveryspan220000---229999-fsfilter-system-recovery"></a><span id="220000_-_229999__FSFilter_System_Recovery"></span><span id="220000_-_229999__fsfilter_system_recovery"></span><span id="220000_-_229999__FSFILTER_SYSTEM_RECOVERY"></span>220000-229999:FSFilter システムの回復

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| file_protector.sys | 227000 | Acronis |
| fbwf.sys | 226000 | マイクロソフト |
| Klsysrec.sys | 221500 | Kaspersky ラボ |
| SFDRV します。SYS | 221400 | Utixo LLC |
| sp_prot.sys | 221300 | Xacti Corporation |
| nsfilep.sys | 221200 | Netsupport Limited |
| syscow.sys | 221100 | [Ok] をシステム AB |
| fsredir.sys | 221000 | マイクロソフト |

## <a name="span-id200000-209999fsfilterclusterfilesystemspanspan-id200000-209999fsfilterclusterfilesystemspanspan-id200000-209999fsfilterclusterfilesystemspan200000---209999-fsfilter-cluster-file-system"></a><span id="200000_-_209999__FSFilter_Cluster_File_System"></span><span id="200000_-_209999__fsfilter_cluster_file_system"></span><span id="200000_-_209999__FSFILTER_CLUSTER_FILE_SYSTEM"></span>200000-209999:FSFilter クラスター ファイル システム

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| CVCBT.sys | 203400 | CommVault Systems, inc. |
| ResumeKeyFilter.sys | 202000 | マイクロソフト |

## <a name="span-id180000-189999fsfilterhsmspanspan-id180000-189999fsfilterhsmspanspan-id180000-189999fsfilterhsmspan180000---189999-fsfilter-hsm"></a><span id="180000_-_189999__FSFilter_HSM"></span><span id="180000_-_189999__fsfilter_hsm"></span><span id="180000_-_189999__FSFILTER_HSM"></span>180000-189999:FSFilter HSM

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| wcifs.sys | 189900 | マイクロソフト |
| prjflt.sys | 189800 | マイクロソフト |
| gameflt.sys | 189750 | マイクロソフト |
| nvmsqrd.sys | 188900 | NVIDIA Corporation |
| RsFlt.sys | 187000 | Redstor Limited |
| mnefs.sys | 186800 | ニッポン Techno ラボ |
| Svfsf.sys | 186700 | Spharsoft テクノロジ |
| uVaultFlt.sys | 186650 | DOR |
| syncmf.sys | 186620 | 酸素クラウド |
| gwmemory.sys | 186600 | Macrotec LLC |
| cteraflt.sys | 186550 | CTERA ネットワーク ltd. |
| dbx.sys | 186500 | Dropbox inc. |
| quaddrasi.sys | 186400 | Quaddra ソフトウェア |
| gdrive.sys | 186300 | Google |
| CoreSyncFilter.sys | 186250 | Adobe Systems inc. |
| EaseTag.sys | 186200 | EaseVault Technologies inc. |
| hcminifilter.sys | 186100 | 満足クラウド inc. |
| PDFsFilter.sys | 186000 | Raxco Sfotware inc. |
| camino.sys | 185900 | CaminoSoft Corp |
| C2C_AF1R します。SYS | 185810 | C2C システム |
| DFdriver.sys | 185800 | DataFirst Corporation |
| amfadrv.sys | 185700 | Quest Software inc. |
| HSMdriver.sys | 185600 | Wim Vervoorn |
| kdfilter.sys | 185555 | Komprise inc. |
| htdafd.sys | 185500 | ブリッジヘッド ソフト |
| odphflt.sys | 180455 | マイクロソフト |
| cldflt.sys | 180451 | マイクロソフト |
| SymHsm.sys | 185400 | Symantec |
| evmf.sys | 185100 | Symantec |
| otfilter.sys | 185000 | 倍音ソフト |
| ithsmdrv.sys | 184900 | IBM |
| MfaFilter.sys | 184800 | Waterford テクノロジ |
| SonyHsmMinifilter.sys | 184700 | Sony Corporation |
| acahsm.sys | 184600 | 自律性 Corporation |
| zlhsm.sys | 184500 | ZL テクノロジ |
| CFileProtect.sys | 184100 | Zhejiang セキュリティ テクノロジ |
| stc_restore_filter.sys | 184000 | StorageCraft テクノロジ |
| dvfilter.sys | 183003 | マイクロソフト |
| Accesstracker.sys | 183002 | マイクロソフト |
| Changetracker.sys | 183001 | マイクロソフト |
| Fstier.sys | 183000 | マイクロソフト |
| hsmcdpflt.sys | 182700 | Metalogix 社 |
| archivmgr.sys | 182690 | Metalogix 社 |
| ntps_oddm.sys | 182600 | NTP ソフトウェア |
| XDFileSys.sys | 182500 | XenData Limited |
| upmjit.sys | 182400 | Citrix システム |
| AtmosFS.sys | 182310 | EMC Corporation |
| DxSpy.sys | 182300 | EMC Software inc. |
| car_hsmflt.sys | 182200 | Caringo, inc. |
| BRDriver.sys | 182100 | BitRaider |
| BRDriver64.sys | 182100 | BitRaider |
| autnhsm.sys | 182000 | 自律性 Corporation |
| cthsmflt.sys | 181970 | ComTrade |
| NxMini.sys | 181900 | NEXSAN 製 |
| neuflt.sys | 181818 | NeuShield |
| npfdaflt.sys | 181800 | Mimosa Systems Inc |
| AppStream.sys | 181700 | アプリケーション ストリーム, inc. |
| HPEDpHsmX64.sys | 181620 | Hewlett-Packard、co. |
| HPArcHsmX64.sys | 181610 | Hewlett-Packard、co. |
| hphsmflt.sys | 181600 | Hewlett-Packard、co. |
| cparchsm.sys | 181610 | Micro Focus |
| RepHsm.sys | 181500 | Double-take ソフトウェア、Inc. |
| RepSIS.sys | 181490 | Double-take ソフトウェア |
| SquashCompressionFsFilter.sys | 181410 | スカッシュ圧縮 |
| GXHSM.sys | 181400 | Commvault Systems, Inc |
| EdsiHsm.sys | 181300 | エンタープライズ データ ソリューション, inc. |
| BkfMap.sys | 181200 | データ記憶域グループ |
| hsmfilter.sys | 181100 | GRAU データ記憶域の可用性グループ |
| mwilcflt.sys | 181020 | Moonwalk ユニバーサル P/L |
| mwilsflt.sys | 181010 | Moonwalk ユニバーサル P/L |
| mwidmflt.sys | 181000 | Moonwalk ユニバーサル P/L |
| HcpAwfs.sys | 181960 | Hitachi |
| sdrefltr.sys | 180950 | Hitachi |
| fltasm.sys | 180900 | グローバル 360 |
| cnet_hsm.sys | 180850 | Carroll Net inc. |
| pntvolflt.sys | 180800 | ポイントのソフトウェアとシステム |
| appxstrm.sys | 180710 | マイクロソフト |
| wimmount.sys | 180700 | マイクロソフト |
| hsmflt.sys | 180600 | マイクロソフト |
| dfsrflt.sys | 180500 | マイクロソフト |
| StorageSyncGuard.sys | 180465 | マイクロソフト |
| StorageSync.sys | 180460 | マイクロソフト |
| dedup.sys | 180450 | マイクロソフト |
| dfmflt.sys | 180410 | マイクロソフト |
| sis.sys | 180400 | マイクロソフト |
| rbt_wfd.sys | 180300 | Inc、riverbed テクノロジ |

## <a name="span-id170000-174999fsfilterimagingexzipspanspan-id170000-174999fsfilterimagingexzipspanspan-id170000-174999fsfilterimagingexzipspan170000---174999-fsfilter-imaging-ex-zip"></a><span id="170000_-_174999__*FSFilter_Imaging_(ex:_.ZIP)"></span><span id="170000_-_174999__*fsfilter_imaging_(ex:_.zip)"></span><span id="170000_-_174999__*FSFILTER_IMAGING_(EX:_.ZIP)"></span>170000-174999: * FSFilter イメージング (例: です。ZIP)

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| pfmfs_ ビルダー。sys | 172100 | Pismo Technic Inc |
| virtual_file.sys | 172000 | Acronis |
| wimFltr.sys | 170500 | マイクロソフト |

## <a name="span-id160000-169999fsfiltercompressionspanspan-id160000-169999fsfiltercompressionspanspan-id160000-169999fsfiltercompressionspan160000---169999-fsfilter-compression"></a><span id="160000_-_169999__FSFilter_Compression"></span><span id="160000_-_169999__fsfilter_compression"></span><span id="160000_-_169999__FSFILTER_COMPRESSION"></span>160000-169999:FSFilter 圧縮

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| CmgFFC.sys | 166000 | Credant テクノロジ |
| compress.sys | 165000 | マイクロソフト |
| cmpflt.sys | 162000 | マイクロソフト |
| IridiumIO.sys | 161700 | Confio |
| logcompressor.sys | 161600 | VelociSQL inc. |
| GcfFilter.sys | 161500 | GemacmbH |
| ssddoubler.sys | 161400 | Sinan Karaca |
| Sptcmp.sys | 161300 | Safend |
| wimfsf.sys | 161000 | マイクロソフト |
| GEFCMP.sys | 160100 | Symantec |

## <a name="span-id140000-149999fsfilterencryptionspanspan-id140000-149999fsfilterencryptionspanspan-id140000-149999fsfilterencryptionspan140000---149999-fsfilter-encryption"></a><span id="140000_-_149999__FSFilter_Encryption"></span><span id="140000_-_149999__fsfilter_encryption"></span><span id="140000_-_149999__FSFILTER_ENCRYPTION"></span>140000-149999:FSFilter 暗号化

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| FJSeparettiFilterRamMon.sys | 149100 | 富士通 |
| psatfilter.sys | 149050 | ProYuga |
| RdFilter.sys | 149040 | CyberEye Research Labs |
| gisfile_decryption.sys | 149030 | 通信 U 中国 |
| TIFSFilter.sys | 149020 | SG Corporation |
| OsrDt2.sys | 149010 | 情報セキュリティ Corp |
| EasyKryptMF.sys | 149000 | SoftKrypt LLC |
| padlock.sys | 148910 | IntSoft inc. |
| ffecore.sys | 148900 | Winmagic |
| fangcloud.sys | 148860 | Hangzhou Yifangyun |
| klvfs.sys | 148810 | Kaspersky ラボ |
| Klfle.sys | 148800 | Kaspersky ラボ |
| ISFP.sys | 148701 | ALPS システム統合 |
| ISIRM.sys | 148700 | ALPS システム統合 CO します。 |
| ASUSSecDrive.sys | 148650 | ASU |
| ABFilterDriver.sys | 148640 | AlertBoot |
| QDocumentFSF.sys | 148630 | BicDroid inc. |
| bfusbenc.sys | 148620 | bitFence inc. |
| sztgbfsf.sys | 148610 | SaferZone co. |
| mwIPSDFilter.sys | 148600 | Egis Technology Inc. |
| csccvdrv.sys | 148500 | Computer Sciences Corporation |
| aefs.sys | 148400 | Angelltech Corporation Xi'an |
| VTEFsFlt.sys | 148374 | EsComputer Corp |
| IWCSEFlt.sys | 148300 | InfoWatch |
| GDDmk.sys | 148250 | G データ Software AG |
| clcxcore.sys | 148210 | ねぇ Solutions Inc. |
| OrisLPDrv.sys | 148200 | CGS Tech の発行 |
| nlemsys.sys | 148100 | NETLIB |
| prvflder.sys | 148000 | マイクロソフト |
| ssefs.sys | 147900 | SecuLution GmbH |
| SePSed.sys | 147800 | ブーンというヘッド, inc. |
| dlmfencx.sys | 147700 | データ暗号化 Ltd |
| SkyDEnc.sys | 147620 | 空の Co Ltd |
| psgcrypt.sys | 147610 | ヨコガワ研究 L Corp |
| bbfsflt.sys | 147600 | Bloombase |
| qx10efs.sys | 147500 | Quixxant |
| MEfefs.sys | 147400 | Eruces inc. |
| medlpflt.sys | 147310 | チェック ポイント Software Technologies Ltd |
| dsfa.sys | 147308 | チェック ポイント Software Technologies Ltd |
| Snicrpt.sys | 147300 | Systemneeds, Inc |
| iCrypt.sys | 147200 | デバイスの入出力データ、INC. |
| xdrmflt.sys | 147100 | bluefinsystems |
| dyFsFilter.sys | 147000 | Scrypto メディア |
| thinairwin.sys | 146960 | シン空気 Inc" |
| UcaDataMgr.sys | 146950 | AppSense Ltd |
| zesocc.sys | 146900 | Novell |
| mfprom.sys | 146800 | McAfee Inc |
| MfeEEFF.sys | 146790 | McAfee inc. |
| intefs.sys | 146700 | TianYu ソフトウェア |
| leofs.sys | 146600 | Leotech |
| autocryptater.sys | 146500 | Richard、物理的 |
| WavxDMgr.sys | 146400 | Scott Cochrane |
| eedmkxp32.sys | 146300 | Entrust |
| SbCe.sys | 146200 | セーフ ブート |
| iSharedFsFilter | 146100 | Packeteer Inc |
| dlrmenc.sys | 146010 | DESlock |
| dlmfenc.sys | 146000 | DESlock |
| aksdf.sys | 145900 | アラジンジャパン |
| DDSFilter.sys | 145800 | WuHan Forworld ソフトウェア |
| SecureShield.sys | 145700 | HMI |
| AifaFE.sys | 145600 | Alfa |
| GBFsMf.sys | 145500 | GreenBorder |
| jmefs.sys | 145400 | 上海発電 |
| emugufs.sys | 145333 | Emugu セキュリティで保護された FS |
| VFDriver.sys | 145300 | R システム |
| IntelDG.sys | 145250 | Intel Corporation |
| DPMEncrypt.sys | 145240 | Randtronics Pty |
| EVSDecrypt64.sys | 145230 | Fortium Technologies Ltd |
| skycryptorencfs.sys | 145220 | Onecryptor CJSC します。 |
| AisLeg.sys | 145210 | 保証された情報セキュリティ |
| windtalk.sys | 145200 | Hyland ソフトウェア |
| TeamCryptor.sys | 145190 | iTwin Pte します。 Ltd. |
| CVDLP.sys | 145180 | CommVault Systems, inc. |
| 5nine.encryptor.sys | 145170 | 5 nine Software inc. |
| ctpfile.sys | 145160 | 北京 Wondersoft テクノロジ co. |
| DPDrv.sys | 145150 | IBM 日本 |
| tsdlp.sys | 145140 | Forware |
| KCDriver.sys | 145130 | Tallegra Ltd |
| CmgFFE.sys | 145120 | Credant テクノロジ |
| fgcenc.sys | 145110 | Fortres Grand corp. |
| sview.sys | 145100 | Cinea |
| TalkeyFilterDriver.sys | 145040 | myTALKEY s.r.o. |
| FedsFilterDriver.sys | 145010 | 物理光 Corp |
| stocc.sys | 145000 | Senforce テクノロジ |
| SnEfs.sys | 144900 | Informzaschita |
| ewSecureDox | 144800 | Echoworx Corporation |
| osrdmk.sys | 144700 | OSR オープン システム リソース, inc. |
| uldcr.sys | 144600 | NCR の財務ソリューション |
| Tkefsxp.sys - 32 ビット | 144500 | インカ インターネット co., Ltd |
| Tkefsxp64.sys - 64 ビット | 144500 | インカ インターネット co., Ltd |
| NmlAccf.sys | 144400 | NEC システム テクノロジ, ltd. |
| SolCrypt.sys | 144300 | Soliton システム株式会社 |
| IngDmk.sys | 144200 | Ingrian Networks, inc. |
| llenc.sys | 144100 | SecureAxis ソフトウェア |
| SecureData.sys | 144030 | SecureAge テクノロジ |
| lockcube.sys | 144020 | SecureAge テクノロジ Pte Ltd |
| sdmedia.sys | 144010 | SecureAge テクノロジ |
| mysdrive.sys | 144000 | SecureAge テクノロジ |
| FileArmor.sys | 143900 | モバイルの防御 |
| VSTXEncr.sys | 143800 | Technologies, Inc. を介して |
| dgdmk.sys | 143700 | Verdasys inc. |
| shandy.sys | 143600 | Safend ltd. |
| C2knet.sys | 143520 | Secuware |
| C2kdef.sys | 143510 | Secuware |
| ssfFS.sys | 143500 | SECUWARE S.L. |
| PISRFE.sys | 143400 | Jilin 大学の IT co. |
| bapfecre.sys | 143300 | BitArmor Systems, Inc |
| KPSD.sys | 143200 | cihosoft |
| Fcfileio.sys | 143100 | Ltd. Brainzsquare、co. |
| cpdrm.sys | 143000 | Pikewerks |
| vmfiltr.sys | 142900 | Vormetric Inc |
| VFSEnc.sys | 142811 | Symantec |
| pgpfs.sys | 142810 | Symantec |
| fencry.sys | 142800 | Symantec |
| TmFileEncDmk.sys | 142700 | Trend Micro Inc |
| cpefs.sys | 142600 | Crypto Pro |
| dekfs.sys | 142500 | KasherLab co., ltd |
| qlockfilter.sys | 142400 | Binqsoft inc. |
| RRFilterDriverStack_d3.sys | 142300 | 合理的な保有期間 |
| cve.sys | 142200 | Absolute Software Corp. |
| spcflt.sys | 142100 | FUJITSU BSC inc. |
| ldsecusb.sys | 142000 | LANDesk inc. |
| fencr.sys | 141900 | SODATSW spol します。 s.r.o. |
| RubiFlt.sys | 141800 | 日立 |
| mfild.sys | 141660 | Penta セキュリティ システム |
| cbfsfilter2017.sys | 141635 | オートマトン Inc |
| cbfsfilter2017.sys | 141634 | オートマトン Inc |
| cbfsfilter2017.sys | 141633 | オートマトン Inc |
| cbfsfilter2017.sys | 141632 | オートマトン Inc |
| cbfsfilter2017.sys | 141631 | オートマトン Inc |
| cbfsfilter2017.sys | 141630 | オートマトン Inc |
| TypeSquare.sys | 141620 | Morisawa inc。 |
| xbdocfilter.sys | 141610 | Zrxb |
| EVSDecrypt32.sys | 141600 | Fortium Technologies Ltd |
| EVSDecrypt64.sys | 141600 | Fortium Technologies Ltd |
| EVSDecryptia64.sys | 141600 | Fortium Technologies Ltd |
| SophosDt2.sys | 141510 | Sophos Plc |
| afdriver.sys | 141500 | ATUS Technology LLC |
| TrivalentFSFltr.sys | 141430 | サイバー依存 |
| CmdMnEfs.sys | 141420 | Comodo セキュリティ |
| DWENxxxx.sys | 141410 | SciencePark Corporation |
| DWENxxxx.sys | 141400 | SciencePark Corporation |
| hdFileSentryDrv32.sys | 141300 | Heilig 防御 |
| hdFileSentryDrv64.sys | 141300 | Heilig 防御 |
| CovertxFilter.sys | 141240 | Micro Focus |
| cplcdt2.sys | 141230 | conpal GmbH |
| asCryptoFilter.sys | 141220 | 適用されたセキュリティ GmbH |
| NetCryptKR.sys | 141210 | NetCrypt Pty Ltd |
| BHFilter.sys | 141200 | 活動の拠点のソリューション |
| Filecrypt.sys | 141100 | マイクロソフト |
| encrypt.sys | 141010 | マイクロソフト |
| swapBuffers.sys | 141000 | マイクロソフト |

## <a name="span-id130000-139999fsfiltervirtualizationspanspan-id130000-139999fsfiltervirtualizationspanspan-id130000-139999fsfiltervirtualizationspan130000---139999-fsfilter-virtualization"></a><span id="130000_-_139999__FSFilter_Virtualization"></span><span id="130000_-_139999__fsfilter_virtualization"></span><span id="130000_-_139999__FSFILTER_VIRTUALIZATION"></span>130000-139999:FSFilter 仮想化

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| Klvirt.sys | 138100 | Kaspersky ラボ |
| VMagic.sys | 138050 | AI のコンサルティング |
| GetSAS.sys | 138040 | SAS Institute Inc |
| rqtNos.sys | 138030 | ReaQta ltd. |
| HIPS64.sys | 138020 | Recrypt LLC |
| frxdrv.sys | 138010 | FSLogix inc. |
| vzdrv.sys | 138000 | Altiris |
| sffsg.sys | 137990 | ヒトデ ストレージ Corp |
| AppStream.sys | 137920 | Symantec |
| Rasm.sys | 137915 | OpDesk Inc |
| boxifier.sys | 137910 | Kenubi |
| xorw.sys | 137900 | CA (XOsoft) |
| ctlua.sys | 137800 | SurfRight B.V. |
| fgccow.sys | 137700 | Fortres Grand corp. |
| aswSnx.sys | 137600 | ALWIL Software |
| AppIsoFltr.sys | 137500 | カーネル ドライバー |
| ptcvfsd.sys | 137400 | PTC |
| BDSandBox.sys | 137300 | BitDefender SRL |
| sxfpss virt.sys | 137200 | Skanix AS |
| DKRtWrt.sys | 137100 | Diskeeper Corporation |
| ivm.sys | 137000 | RingCube テクノロジ |
| ivm.sys | 136990 | Citrix システム |
| dtiof.sys | 136900 | Instavia Software inc. |
| NxTopCP.sys | 136800 | 仮想 Ccomputer inc. |
| svdriver.sys | 136700 | VMware, inc. |
| unifltr.sys | 136600 | Unidesk |
| unidrive.sys (名前) | 136600 | Unidesk |
| unirsd.sys | 136600 | Unidesk |
| ive.sys | 136500 | TrendMicro inc. |
| odamf.sys | 136450 | Sony Corporation |
| SrMxfMf.sys | 136440 | Sony Corporation |
| pszmf.sys | 136430 | Sony Corporation |
| sxsudfmf.sys | 136410 | Sony Corporation |
| vfammf.sys | 136400 | Sony Corporation |
| VHDFlt.sys | 136240 | Dell |
| VHDFlt.sys | 136230 | Dell |
| VHDFlt.sys | 136220 | Dell |
| VHDFlt.sys | 136210 | Dell |
| ncfsfltr.sys | 136200 | NComputing inc. |
| cmdguard.sys | 136100 | COMODO Security Solutions Inc |
| hpfsredir.sys | 136000 | HP |
| svhdxflt.sys | 135100 | マイクロソフト |
| luafv.sys | 135000 | マイクロソフト |
| ivm.sys | 134000 | RingCube テクノロジ |
| ivm.sys | 133990 | Citrix システム |
| frxdrvvt.sys | 132700 | FSLogix inc. |
| pfmfs_ ビルダー。sys | 132600 | Pismo Technic inc. |
| Stcvhdmf.sys | 132600 | StorageCraft Tech Corp |
| appdrv01.sys | 132500 | 保護テクノロジ |
| virtual_file.sys | 132400 | Acronis |
| pdiFsFilter.sys | 132300 | 位 Data inc. |
| avgvtx86.sys | 132200 | AVG テクノロジ CZ |
| avgvtx64.sys | 132200 | AVG テクノロジ CZ |
| DataNet_Driver.sys | 132100 | AppSense Ltd |
| EgenPage.sys | 132000 | Egenera, inc. |
| unidrive.sys 古い | 131900 | Unidesk |
| ivm.sys.old | 131800 | RingCube テクノロジ |
| XiaobaiFsR.sys | 131710 | 深川 UNNOO LTD |
| XiaobaiFs.sys | 131700 | 深川 UNNOO LTD |
| iotfsflt.sys | 131600 | IO タービン Inc |
| mhpvfs.sys | 131500 | Wunix Limited |
| svdriver.sys | 131400 | SnapVolumes inc. |
| Sptvrt.sys | 131300 | Safend |
| antirswf.sys | 131210 | Panzor サイバー セキュリティ |
| aicvirt.sys | 131200 | AI のコンサルティング |
| sfo.sys | 130100 | マイクロソフト |
| DeVolume.sys | 130000 | マイクロソフト |

## <a name="span-id120000-129999fsfilterphysicalquotamanagementspanspan-id120000-129999fsfilterphysicalquotamanagementspanspan-id120000-129999fsfilterphysicalquotamanagementspan120000---129999-fsfilter-physical-quota-management"></a><span id="120000_-_129999__FSFilter_Physical_Quota_management"></span><span id="120000_-_129999__fsfilter_physical_quota_management"></span><span id="120000_-_129999__FSFILTER_PHYSICAL_QUOTA_MANAGEMENT"></span>120000-129999:FSFilter 物理クォータの管理

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| quota.sys | 125000 | マイクロソフト |
| どちら | 124000 | Veritas |
| DroboFlt.sys | 123900 | データのロボット工学 |

## <a name="span-id100000-109999fsfilteropenfilespanspan-id100000-109999fsfilteropenfilespanspan-id100000-109999fsfilteropenfilespan100000---109999-fsfilter-open-file"></a><span id="100000_-_109999__FSFilter_Open_File"></span><span id="100000_-_109999__fsfilter_open_file"></span><span id="100000_-_109999__FSFILTER_OPEN_FILE"></span>100000-109999:開いている FSFilter ファイル

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| insyncmf.sys | 105000 | InSync |
| SPILock8.sys | 100900 | Software Pursuits inc. |
| Klbackupflt.sys | 100800 | Kaspersky |
| repkap | 100700 | ビジョン ソリューション |
| symrg.sys | 100600 | Symantec |
| adsfilter.sys | 100500 | PolyServ |

## <a name="span-id80000-89999fsfiltersecurityenhancerspanspan-id80000-89999fsfiltersecurityenhancerspanspan-id80000-89999fsfiltersecurityenhancerspan80000---89999-fsfilter-security-enhancer"></a><span id="80000_-_89999__FSFilter_Security_Enhancer"></span><span id="80000_-_89999__fsfilter_security_enhancer"></span><span id="80000_-_89999__FSFILTER_SECURITY_ENHANCER"></span>80000-89999:FSFilter セキュリティ強化

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| psprotf.sys | 88210 | Panzor サイバー セキュリティ |
| DPMACL.sys | 88100 | Randtronics Pty |
| dsbwnck.sys | 88000 | 簡単なソリューション inc. |
| cbfsfilter2017.sys | 87910 | オートマトン |
| cbfsfilter2017.sys | 87909 | オートマトン Inc |
| cbfsfilter2017.sys | 87908 | オートマトン Inc |
| cbfsfilter2017.sys | 87907 | オートマトン Inc |
| cbfsfilter2017.sys | 87906 | オートマトン Inc |
| cbfsfilter2017.sys | 87905 | オートマトン Inc |
| cbfsfilter2017.sys | 87904 | オートマトン Inc |
| cbfsfilter2017.sys | 87903 | オートマトン Inc |
| cbfsfilter2017.sys | 87902 | オートマトン Inc |
| cbfsfilter2017.sys | 87901 | オートマトン Inc |
| cbfsfilter2017.sys | 87900 | オートマトン Inc |
| rsbfsfilter.sys | 87800 | Corel Corporation |
| hsmltflt.sys | 87720 | 日立ソリューション |
| hssfflt.sys | 87710 | 日立ソリューション |
| acmnflt.sys | 87708 | 日立ソリューション |
| ACSKFFD.sys | 87700 | 日立ソリューション |
| MyDLPMF.sys | 87600 | Comodo グループ inc. |
| ScuaRaw.sys | 87500 | SCUA Seguran&#231;da 情報&#231;&#227;o |
| HDSFilter.sys | 87400 | NeoAutus オートメーション システム |
| ikfsmflt.sys | 87300 | IronKey inc. |
| Klsec.sys | 87200 | Kaspersky ラボ |
| XtimUSBFsFilterDrv.sys | 87190 | 大連 CP SDT Ltd |
| RGFLT_FM.sys | 87180 | Hauri.inc |
| flockflt.sys | 87170 | Ahranta inc. |
| ZdCore.sys | 87160 | Zend 技術ソリューション |
| dcrypt.sys | 87150 | ReactOS Foundation |
| hpradeo.sys | 87140 | Pradeo |
| SDFSAGDRV します。SYS | 87130 | ALPS システム統合 CO します。 |
| SDFSDEVFDRV します。SYS | 87120 | ALPS システム統合 CO します。 |
| SDIFSFDRV します。SYS | 87110 | ALPS システム統合 CO します。 |
| SDFSFDRV します。SYS | 87100 | ALPS システム統合 CO します。 |
| CModule.sys | 87070 | Zhejiang セキュリティ テクノロジ |
| HHRRPH.sys | 87010 | ソフトウェア H + H GmbH |
| HHVolFltr.sys | 87000 | ソフトウェア H + H GmbH |
| SbieDrv.sys | 86900 | Sandboxie L.T.D |
| assetpro.sys | 86800 | pyaprotect&#x2024;com |
| dlp.sys | 86700 | Tellus ソフトウェア AS |
| eps.sys | 86600 | Lumension セキュリティ |
| RapportPG64.sys | 86500 | Trusteer |
| amminifilter.sys | 86400 | AppSense |
| Sniflt.sys | 86300 | Systemneeds, Inc |
| SecFile.sys | 86200 | デザイン Inc. によってセキュリティ保護します。 |
| philly.sys | 86110 | triCerat inc. |
| reggy.sys | 86100 | triCerat inc. |
| cygfilt.sys | 86000 | Livegrid が組み込まれています |
| prelaunch.sys | 85900 | D3L |
| csareg.sys | 85810 | Cisco Systems |
| csaenh.sys | 85800 | Cisco Systems |
| asEpsDrv.sys | 85750 | ASHINI co. ltd. |
| CIDACL.sys | 85700 | GE 航空 (デジタル システム Germantown) |
| CVDLP.sys | 85610 | CommVault Systems, inc. |
| QGPEFlt.sys | 85600 | Quest Software |
| Drveng.sys | 85500 | CA |
| vracfil2.sys | 85400 | ハウリジャパン |
| TFsDisk.sys | 85300 | Teruten |
| rcMiniDrv.sys | 85200 | REDGATE CO., LTD. |
| SnMc5xx.sys | 85100 | Informzaschita |
| FSPFltd.sys | 85010 | Alfa |
| AifaFFP.sys | 85000 | Alfa |
| EsAccCtlFE.sys | 84901 | EgoSecure GmbH |
| DpAccCtl.sys | 84900 | Softbroker GmbH |
| privman.sys | 84800 | BeyondTrust |
| eumntvol.sys | 84700 | Eugrid Inc |
| SoloEncFilter.sys | 84600 | Soliton システム |
| sbfilter.sys | 84500 | UC4 ソフトウェア |
| cposfw.sys | 84450 | チェック ポイント Software Technologies Ltd |
| vsdatant.sys | 84400 | ゾーン Labs LLC |
| SePnet.sys | 84350 | ブーンというヘッド, inc. |
| SePuld.sys | 84340 | ブーンというヘッド, inc. |
| SePpld.sys | 84330 | ブーンというヘッド, inc. |
| SePfsd.sys | 84320 | ブーンというヘッド, inc. |
| SePwld.sys | 84310 | ブーンというヘッド, inc. |
| SePprd.sys | 84300 | ブーンというヘッド, inc. |
| InPFlter.sys | 84200 | ブーンというヘッド, inc. |
| CProCtrl.sys | 84100 | Crypto Pro |
| spyshelter.sys | 84000 | Datpol |
| clpinspprot.sys | 83900 | 情報技術企業 ltd. |
| uvmfsflt.sys | 83376 | NEC Corporation  |
| ProtectIt.sys | 82373 | テラバイト inc. |
| dguard.sys | 82300 | Dmitry Varshavsky |
| NSUSBStorageFilter.sys | 82200 | NetSupport Ltd |
| RMSEFFMV します。SYS | 82100 | CJSC Returnil ソフトウェア |
| BoksFLAC.sys | 82000 | Fox テクノロジ |
| cpAcOnPnP.sys | 81910 | conpal GmbH |
| cpsgfsmf.sys | 81900 | conpal GmbH |
| ndevsec.sys | 81800 | Norman ASA |
| ViewIntus_RTDG.sys | 81700 | Pentego Technologies Ltd |
| airlock.sys | 81630 | エアロック デジタル Pty Ltd |
| zam.sys | 81620 |  |
| ANXfsm.sys | 81610 | Arcdo |
| CDrSDFlt.sys | 81600 | Arcdo |
| crnselfdefence32.sys | 81500 | Coranti inc. |
| crnselfdefence64.sys | 81500 | Coranti inc. |
| zlock_drv.sys | 81400 | み |
| f101fs.sys | 81300 | Fortres Grand corp. |
| sysgar.sys | 81200 | 中核のデータの回復 |
| EmbargoM.sys | 81100 | ScriptLogic |
| ngssdef.sys | 81050 | Wontok Inc |
| ssb.sys | 81041 | Wontok Inc |
| regflt.sys | 81040 | Wontok Inc |
| fsds2a.sys | 81000 | Splitstreem Ltd |
| csacentr.sys | 80900 | Cisco Systems |
| ScvFLT50.sys | 80850 | Secuve Ltd |
| paritydriver.sys | 80800 | Bit9, inc. |
| nkfsprot.sys | 80710 | Konneka |
| nkprot.sys | 80700 | KONNEKA インフォメーション テクノロジ |
| acpadlock.sys | 80691 | IntSoft Co |
| ksmf.sys | 80690 | IntSoft Co |
| im.sys | 80680 | CrowdStrike |
| SophosED.sys | 80670 | Sophos |
| jazzfile.sys | 80660 | ジャズ ネットワーク |
| SMXFs.sys | 80500 | OSR |

## <a name="span-id60000-69999fsfiltercopyprotectionspanspan-id60000-69999fsfiltercopyprotectionspanspan-id60000-69999fsfiltercopyprotectionspan60000---69999-fsfilter-copy-protection"></a><span id="60000_-_69999__FSFilter_Copy_Protection"></span><span id="60000_-_69999__fsfilter_copy_protection"></span><span id="60000_-_69999__FSFILTER_COPY_PROTECTION"></span>60000-69999:FSFilter コピー防止

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| d3clock.sys | 67000 | D3CRYPT3D LLC |
| cbfltfs4.sys | 66500 | I3D テクノロジ Inc |
| CkProcess.sys | 66100 | KASHU システム デザイン INC. |
| dlmfprot.sys | 66000 | データ暗号化 Sys |
| baprtsef.sys | 65700 | BitArmor Systems, Inc |
| sxfpss.sys | 65600 | Skanix AS |
| rgasdev.sys | 65500 | Macrovision |
| SkyFPDrv.sys | 65410 | 空の co. ltd. |
| SkyLWP.sys | 65400 | 空の co. ltd. |
| SnEraser.sys | 65300 | Informzaschita |
| vfilter.sys | 65200 | RSJ ソフトウェア GmbH |
| COGOFlt32.sys | 65100 | Fortium Technologies Ltd |
| COGOFlt64.sys | 65100 | Fortium Technologies Ltd |
| COGOFLTia64.sys | 65100 | Fortium Technologies Ltd |
| scrubber.sys | 65000 | マイクロソフト |
| BRDriver.sys | 64000 | BitRaider LLC |
| BRDriver64.sys | 64000 | BitRaider LLC |
| X7Ex.sys | 62500 | Exent Technologies Ltd |
| LibertyFSF.sys | 62300 | Bayalink ソリューション Co |
| axfsdrv2.sys | 62100 | Axence Software inc. |
| sds.sys | 62000 | エグレス ソフトウェア |
| TotalSystemAuditor.sys | 61600 | ANRC LLC |
| MBAMApiary.sys | 61500 | Malwarebytes corp. |
| WA_FSW.sys | 61400 | として Administraci&#243;n y Mejoramiento |
| ViewIntus_RTAS | 61300 | Pentego テクノロジ |
| tffac.sys | 61200 | Toshiba Corporation |
| tccp.sys | 61100 | TrusCont Ltd |
| KomFS.sys | 61000 | KOM ネットワーク |

## <a name="span-id40000-49999fsfilterbottomspanspan-id40000-49999fsfilterbottomspanspan-id40000-49999fsfilterbottomspan40000---49999-fsfilter-bottom"></a><span id="40000_-_49999__FSFilter_Bottom"></span><span id="40000_-_49999__fsfilter_bottom"></span><span id="40000_-_49999__FSFILTER_BOTTOM"></span>40000-49999:FSFilter 下部

| ミニフィルター                  | 高度 | Company                                 |
------------------------------|----------|-----------------------------------------|
| RMPFileMounter.sys | 48000 | ManageEngine Zoho |
| cbfsfilter2017.sys | 47400 | 12d 相乗効果 |
| pfmfs_ ビルダー。sys | 47300 | Pismo Technic inc. |
| DLDriverMiniFlt.sys | 47200 | DeviceLock Inc |
| hsmltlib.sys | 47110 | 日立ソリューション |
| hskdlib.sys | 47100 | 日立ソリューション |
| acmnlib.sys | 47090 | 日立ソリューション |
| aictracedrv_b.sys | 47000 | AI のコンサルティング |
| hhdcfltr.sys | 46900 | Seagate のテクノロジ |
| Npsvctrig.sys | 46000 | マイクロソフト |
| klvfs.sys | 44900 | Kaspersky ラボ |
| Klbackupflt.sys | 44890 | Kaspersky ラボ |
| rsfxdrv.sys | 41000 | マイクロソフト |
| defilter.sys | 40900 | マイクロソフト |
| AppVVemgr.sys | 40800 | マイクロソフト |
| wofadk.sys | 40730 | マイクロソフト |
| wof.sys | 40700 | マイクロソフト |
| fileinfo | 40500 | マイクロソフト |
| WinSetupBoot.sys | 40400 | マイクロソフト |

## <a name="span-id20000-29999fsfiltersystemspanspan-id20000-29999fsfiltersystemspanspan-id20000-29999fsfiltersystemspan20000---29999-fsfilter-system"></a><span id="20000_-_29999__FSFilter_System"></span><span id="20000_-_29999__fsfilter_system"></span><span id="20000_-_29999__FSFILTER_SYSTEM"></span>20000-29999:FSFilter システム

[なし] :
