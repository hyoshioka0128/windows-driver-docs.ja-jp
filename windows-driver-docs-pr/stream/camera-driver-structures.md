---
title: カメラドライバーの構造
description: 次のカメラドライバー構造は、Windows 10 の新しいものです。
ms.assetid: E1C2695B-F3E3-4B16-9552-C79B957A5470
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8acbc9a2ef060278a26f6ca32398b4e747113ae1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844755"
---
# <a name="camera-driver-structures"></a>カメラドライバーの構造


次のカメラドライバー構造は、Windows 10 の新しいものです。

[**CapturedMetadataExposureCompensation**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagcapturedmetadataexposurecompensation)

[**CapturedMetadataISOGains**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagcapturedmetadataisogains)

[**CapturedMetadataWhiteBalanceGains**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagcapturedmetadatawhitebalancegains)

[**FaceCharacterization**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagfacecharacterization)

[**FaceCharacterizationBlobHeader**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagfacecharacterizationblobheader)

[**Facerの情報**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagfacerectinfo)

[**Facerが Infoblobheader**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagfacerectinfoblobheader)

[**HistogramBlobHeader**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-taghistogramblobheader)

[**HistogramDataHeader**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-taghistogramdataheader)

[**HistogramGrid**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-taghistogramgrid)

[**HistogramHeader**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-taghistogramheader)

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_METADATAINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo)

[**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)

[**KSCAMERA\_EXTENDEDPROP\_プロファイル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_extendedprop_profile)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcaps)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPSHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcapsheader)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_露出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_exposure)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_焦点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_focus)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_info)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrol)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROLHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrolheader)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_ホワイトバランス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_whitebalance)

[**ITEMHEADER\_KSCAMERA\_メタデータ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader)

[**KSCAMERA\_メタデータ\_PHOTOCONFIRMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_photoconfirmation)

[**KSCAMERA\_PERフレーム設定\_CAP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)

[**KSCAMERA\_PERフレーム設定\_CAP\_項目\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_item_header)

[**KSCAMERA\_PERフレーム設定\_カスタム\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_custom_item)

[**KSCAMERA\_PERフレーム設定\_フレーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_frame_header)

[**KSCAMERA\_PERフレーム設定\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_header)

[**KSCAMERA\_PERフレーム設定\_項目\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_item_header)

[**KSCAMERA\_PROFILE\_CONCURRENCYINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_profile_concurrencyinfo)

[**KSCAMERA\_プロファイル\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_profile_info)

[**KSCAMERA\_PROFILE\_MEDIAINFO.XML**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_profile_mediainfo)

[**KSCAMERA\_プロファイル\_PININFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_profile_pininfo)

[**KSDEVICE\_プロファイル\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksdevice_profile_info)

[**KSDEVICE\_THERMAL\_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_thermal_dispatch)

[**KSPIN\_MDL\_キャッシュ\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_mdl_caching_notification)

[**KSPIN\_MDL\_キャッシュ\_NOTIFICATION32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_mdl_caching_notification32)

[**KSK プロパティ\_ステップ実行\_長い**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn936838(v=vs.85))

[**KSK プロパティ\_ステップ実行\_LONGLONG**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn936841(v=vs.85))

[**KSK ストリーム\_メタデータ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_metadata_info)

[**KSK ストリーム\_UVC\_メタデータ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_uvc_metadata)

[**KSK ストリーム\_UVC\_METADATATYPE\_TIMESTAMP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_uvc_metadatatype_timestamp)

[**Metadatのスタンプ**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagmetadatatimestamps)

[**MF\_MDL\_共有\_ペイロード\_キー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_mf_mdl_shared_payload_key)

 

 




