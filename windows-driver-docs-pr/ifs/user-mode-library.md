---
title: ユーザーモード ライブラリ
description: ユーザーモード ライブラリ
ms.assetid: a471ae15-bbdd-47c8-ad77-9b82281dd430
keywords:
- フィルター マネージャー WDK ファイル システム ミニフィルター、ユーザー モード ライブラリ
- ユーザー モード ライブラリ WDK ファイル システム ミニフィルター
- Fltlib.dll
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 018cd26d0cf3a0c9730fbd3be0d238091a27320d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380295"
---
# <a name="user-mode-library"></a>ユーザーモード ライブラリ


フィルター マネージャーのユーザー モード インターフェイスでは、フィルター ドライバーが含まれている製品の共通機能を提供します。 ユーザー モードのライブラリは*Fltlib.dll*します。 アプリケーションがヘッダー ファイルをインクルード*FltUser.h*と*FltUserStructures.h*へのリンクと*FltLib.lib*します。

これらのユーザー モード インターフェイスは、一般的なコントロールのミニフィルター ドライバーと、ユーザー モードのサービスまたはコントロールのプログラムと、フィルター ドライバー間の通信を有効にします。 また、ユーザー モードのインターフェイスは、フィルター、ボリューム、およびインスタンスの列挙を許可する管理ツールのインターフェイスを提供します。

ミニフィルターのユーザー モードの通信 Api には、管理者特権が必要ありません。 ミニフィルターの代わりに、定義が必要な特権を使用して、 [ **ACL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_acl)ポートを定義します。

### <a name="span-idfiltermanageruser-modelibraryroutinesspanspan-idfiltermanageruser-modelibraryroutinesspanspan-idfiltermanageruser-modelibraryroutinesspanfilter-manager-user-mode-library-routines"></a><span id="Filter_Manager_User-Mode_Library_Routines"></span><span id="filter_manager_user-mode_library_routines"></span><span id="FILTER_MANAGER_USER-MODE_LIBRARY_ROUTINES"></span>マネージャーのユーザー モードのライブラリ ルーチンをフィルター処理します。

フィルター マネージャーは、ユーザー モード アプリケーションの読み込みとアンロード ミニフィルター ドライバーを使用するための次サポート ルーチンを提供します。

[**FilterLoad**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterload)

[**FilterUnload**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterunload)

作成とミニフィルター ドライバーおよびインスタンスのハンドルを閉じるには、次のサポート ルーチンが用意されています。

[**FilterClose**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterclose)

[**節**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtercreate)

[**FilterInstanceClose**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterinstanceclose)

[**FilterInstanceCreate**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterinstancecreate)

アタッチとデタッチ ミニフィルター ドライバーのインスタンスには、次のサポート ルーチンが用意されています。

[**FilterAttach**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterattach)

[**FilterAttachAtAltitude**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterattachataltitude)

[**FilterDetach**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterdetach)

次のサポート ルーチンは、フィルター、ボリューム、およびインスタンスを列挙するために用意されています。

[**FilterFindFirst**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterfindfirst)

[**FilterFindNext**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterfindnext)

[**FilterInstanceFindFirst**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterinstancefindfirst)

[**FilterInstanceFindNext**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterinstancefindnext)

[**FilterVolumeFindFirst**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtervolumefindfirst)

[**FilterVolumeFindNext**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtervolumefindnext)

[**FilterVolumeInstanceFindFirst**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtervolumeinstancefindfirst)

[**FilterVolumeInstanceFindNext**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtervolumeinstancefindnext)

情報の照会には、次のサポート ルーチンが用意されています。

[**FilterGetDosName**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtergetdosname)

[**FilterGetInformation**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtergetinformation)

[**FilterInstanceGetInformation**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterinstancegetinformation)

ユーザー操作によって開始された通信には、次のサポート ルーチンが用意されています。

[**FilterConnectCommunicationPort**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterconnectcommunicationport)

[**FilterSendMessage**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtersendmessage)

ミニフィルター ドライバーによって開始された通信に応答するは、次のサポート ルーチンが用意されています。

[**FilterGetMessage**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtergetmessage)

[**FilterReplyMessage**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterreplymessage)

 

 




