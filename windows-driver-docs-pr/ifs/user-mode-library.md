---
title: ユーザーモード ライブラリ
description: ユーザーモード ライブラリ
ms.assetid: a471ae15-bbdd-47c8-ad77-9b82281dd430
keywords:
- フィルターマネージャー WDK ファイルシステムミニフィルター、ユーザーモードライブラリ
- ユーザーモードライブラリ WDK ファイルシステムミニフィルター
- Fltlib .dll
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcc639bfd9e70c04521e48762979a2993a012a3c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840942"
---
# <a name="user-mode-library"></a>ユーザーモード ライブラリ


フィルターマネージャーのユーザーモードインターフェイスは、フィルタードライバーを含む製品に共通の機能を提供します。 ユーザーモードライブラリは*Fltlib .dll*です。 アプリケーションには、ヘッダーファイル*Fltuser .h*と*Fltuserストラクチャー .h*が含まれています。また、 *fltuser*にリンクしています。

これらのユーザーモードインターフェイスを使用すると、ミニフィルタードライバーとユーザーモードサービスまたはコントロールプログラムとフィルタードライバーの間の通信を全般的に制御できます。 ユーザーモードインターフェイスには、フィルター、ボリューム、およびインスタンスの列挙を可能にする管理ツール用のインターフェイスも用意されています。

ミニフィルターの場合、ユーザーモード通信 Api は管理者特権を必要としません。 代わりに、ミニフィルターでは、ポートで定義されている[**ACL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_acl)を使用して必要な特権を定義します。

### <a name="span-idfilter_manager_user-mode_library_routinesspanspan-idfilter_manager_user-mode_library_routinesspanspan-idfilter_manager_user-mode_library_routinesspanfilter-manager-user-mode-library-routines"></a><span id="Filter_Manager_User-Mode_Library_Routines"></span><span id="filter_manager_user-mode_library_routines"></span><span id="FILTER_MANAGER_USER-MODE_LIBRARY_ROUTINES"></span>フィルターマネージャーのユーザーモードライブラリルーチン

フィルターマネージャーには、ミニフィルタードライバーの読み込みとアンロードに使用するユーザーモードアプリケーションの次のサポートルーチンが用意されています。

[**FilterLoad**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterload)

[**FilterUnload**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterunload)

ミニフィルタードライバーとインスタンスハンドルの作成と終了には、次のサポートルーチンが用意されています。

[**FilterClose**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterclose)

[**FilterCreate**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtercreate)

[**FilterInstanceClose**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterinstanceclose)

[**FilterInstanceCreate**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterinstancecreate)

ミニフィルタードライバーインスタンスのアタッチとデタッチには、次のサポートルーチンが用意されています。

[**FilterAttach**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterattach)

[**FilterAttachAtAltitude**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterattachataltitude)

[**FilterDetach**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterdetach)

フィルター、ボリューム、およびインスタンスを列挙するために、次のサポートルーチンが用意されています。

[**FilterFindFirst**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterfindfirst)

[**FilterFindNext**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterfindnext)

[**FilterInstanceFindFirst**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterinstancefindfirst)

[**FilterInstanceFindNext**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterinstancefindnext)

[**FilterVolumeFindFirst**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtervolumefindfirst)

[**FilterVolumeFindNext**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtervolumefindnext)

[**FilterVolumeInstanceFindFirst**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtervolumeinstancefindfirst)

[**FilterVolumeInstanceFindNext**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtervolumeinstancefindnext)

情報を照会するために、次のサポートルーチンが用意されています。

[**FilterGetDosName**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtergetdosname)

[**FilterGetInformation**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtergetinformation)

[**FilterInstanceGetInformation**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterinstancegetinformation)

ユーザー操作によって開始される通信には、次のサポートルーチンが用意されています。

[**FilterConnectCommunicationPort**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterconnectcommunicationport)

[**FilterSendMessage**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtersendmessage)

ミニフィルタードライバーによって開始される通信に応答するために、次のサポートルーチンが用意されています。

[**FilterGetMessage**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtergetmessage)

[**FilterReplyMessage**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterreplymessage)

 

 




