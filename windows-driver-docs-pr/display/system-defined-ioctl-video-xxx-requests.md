---
title: システム定義の IOCTL_VIDEO_XXX 要求
description: システム定義の IOCTL_VIDEO_XXX 要求
ms.assetid: 30309de1-c991-402d-a701-7e88c3367d24
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000、要求の処理
- 要求処理の WDK ビデオのミニポート
- I/O WDK ビデオのミニポート
- システム定義の IOCTL_VIDEO_XXX 要求 WDK ビデオのミニポート
- IOCTL_VIDEO_XXX 要求 WDK のビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c5d7b214e6462ba929ac69f066ad1d8db51a2da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558021"
---
# <a name="system-defined-ioctlvideoxxx-requests"></a>システム定義の IOCTL\_ビデオ\_XXX 要求


## <span id="ddk_system_defined_ioctl_video_xxx_requests_gg"></span><span id="DDK_SYSTEM_DEFINED_IOCTL_VIDEO_XXX_REQUESTS_GG"></span>


通常、ほとんどのビデオのミニポート ドライバーでは、次の要求をサポートします。

[**IOCTL\_ビデオ\_クエリ\_NUM\_利用\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff567824)

[**IOCTL\_ビデオ\_クエリ\_利用\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff567816)

[**IOCTL\_ビデオ\_クエリ\_現在\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff567819)

[**IOCTL\_VIDEO\_SET\_CURRENT\_MODE**](https://msdn.microsoft.com/library/windows/hardware/ff567846)

[**IOCTL\_VIDEO\_RESET\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff567834)

[**IOCTL\_ビデオ\_マップ\_ビデオ\_メモリ**](https://msdn.microsoft.com/library/windows/hardware/ff567812)

[**IOCTL\_ビデオ\_UNMAP\_ビデオ\_メモリ**](https://msdn.microsoft.com/library/windows/hardware/ff568153)

[**IOCTL\_ビデオ\_共有\_ビデオ\_メモリ**](https://msdn.microsoft.com/library/windows/hardware/ff568149)

[**IOCTL\_ビデオ\_共有解除\_ビデオ\_メモリ**](https://msdn.microsoft.com/library/windows/hardware/ff568155)

[**IOCTL\_ビデオ\_クエリ\_パブリック\_アクセス\_範囲**](https://msdn.microsoft.com/library/windows/hardware/ff567829)

[**IOCTL\_ビデオ\_FREE\_パブリック\_アクセス\_範囲**](https://msdn.microsoft.com/library/windows/hardware/ff567796)

[**IOCTL\_ビデオ\_取得\_POWER\_管理**](https://msdn.microsoft.com/library/windows/hardware/ff567803)

[**IOCTL\_ビデオ\_設定\_POWER\_管理**](https://msdn.microsoft.com/library/windows/hardware/ff568148)

[**IOCTL\_ビデオ\_取得\_子\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567801)

[**IOCTL\_ビデオ\_設定\_子\_状態\_構成**](https://msdn.microsoft.com/library/windows/hardware/ff567840)

[**IOCTL\_ビデオ\_検証\_子\_状態\_構成**](https://msdn.microsoft.com/library/windows/hardware/ff568156)

ビデオのミニポート ドライバーは、アダプターの機能に応じて、次の追加の要求をサポートできます。

[**IOCTL\_ビデオ\_クエリ\_色\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff567817)

[**IOCTL\_ビデオ\_設定\_色\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff567842) (デバイスがパレットがかどうかに必要)

[**IOCTL\_ビデオ\_を無効にする\_ポインター**](https://msdn.microsoft.com/library/windows/hardware/ff567786)

[**IOCTL\_ビデオ\_を有効にする\_ポインター**](https://msdn.microsoft.com/library/windows/hardware/ff567793)

[**IOCTL\_ビデオ\_クエリ\_ポインター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff567826)

[**IOCTL\_ビデオ\_クエリ\_ポインター\_ATTR**](https://msdn.microsoft.com/library/windows/hardware/ff567825)

[**IOCTL\_ビデオ\_設定\_ポインター\_ATTR**](https://msdn.microsoft.com/library/windows/hardware/ff568144)

[**IOCTL\_ビデオ\_クエリ\_ポインター\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff567827)

[**IOCTL\_ビデオ\_設定\_ポインター\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff568145)

[**IOCTL\_VIDEO\_HANDLE\_VIDEOPARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff567805)

[**IOCTL\_ビデオ\_スイッチ\_デュアル ビュー**](https://msdn.microsoft.com/library/windows/hardware/ff568151)

次の追加の要求をサポートするためには、VGA と互換性のある SVGA ミニポート ドライバーが必要です。

[**IOCTL\_ビデオ\_保存\_ハードウェア\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567838)

[**IOCTL\_ビデオ\_復元\_ハードウェア\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567835)

[**IOCTL\_ビデオ\_を無効にする\_カーソル**](https://msdn.microsoft.com/library/windows/hardware/ff567784)

[**IOCTL\_ビデオ\_を有効にする\_カーソル**](https://msdn.microsoft.com/library/windows/hardware/ff567788)

[**IOCTL\_ビデオ\_クエリ\_カーソル\_ATTR**](https://msdn.microsoft.com/library/windows/hardware/ff567820)

[**IOCTL\_VIDEO\_SET\_CURSOR\_ATTR**](https://msdn.microsoft.com/library/windows/hardware/ff567847)

[**IOCTL\_ビデオ\_クエリ\_カーソル\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff567821)

[**IOCTL\_ビデオ\_設定\_カーソル\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff567849)

[**IOCTL\_VIDEO\_GET\_BANK\_SELECT\_CODE**](https://msdn.microsoft.com/library/windows/hardware/ff567799)

[**IOCTL\_ビデオ\_設定\_パレット\_を登録します**](https://msdn.microsoft.com/library/windows/hardware/ff568142)

[**IOCTL\_ビデオ\_ロード\_AND\_設定\_フォント**](https://msdn.microsoft.com/library/windows/hardware/ff567809)

見つかる各 IOCTL の詳細に[ビデオのミニポート ドライバー I/O 制御コード](https://msdn.microsoft.com/library/windows/hardware/ff570515)します。 ミニポート ドライバー開発者は、ドキュメントに未記載のシステム定義の Ioctl には使用しないでください。

 

 





