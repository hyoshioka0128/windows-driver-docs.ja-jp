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
ms.openlocfilehash: 01d57cbc7cebe19d46a33505edff7188921fef6f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389597"
---
# <a name="user-mode-library"></a>ユーザーモード ライブラリ


フィルター マネージャーのユーザー モード インターフェイスでは、フィルター ドライバーが含まれている製品の共通機能を提供します。 ユーザー モードのライブラリは*Fltlib.dll*します。 アプリケーションがヘッダー ファイルをインクルード*FltUser.h*と*FltUserStructures.h*へのリンクと*FltLib.lib*します。

これらのユーザー モード インターフェイスは、一般的なコントロールのミニフィルター ドライバーと、ユーザー モードのサービスまたはコントロールのプログラムと、フィルター ドライバー間の通信を有効にします。 また、ユーザー モードのインターフェイスは、フィルター、ボリューム、およびインスタンスの列挙を許可する管理ツールのインターフェイスを提供します。

ミニフィルターのユーザー モードの通信 Api には、管理者特権が必要ありません。 ミニフィルターの代わりに、定義が必要な特権を使用して、 [ **ACL** ](https://msdn.microsoft.com/library/windows/hardware/ff538866)ポートを定義します。

### <a name="span-idfiltermanageruser-modelibraryroutinesspanspan-idfiltermanageruser-modelibraryroutinesspanspan-idfiltermanageruser-modelibraryroutinesspanfilter-manager-user-mode-library-routines"></a><span id="Filter_Manager_User-Mode_Library_Routines"></span><span id="filter_manager_user-mode_library_routines"></span><span id="FILTER_MANAGER_USER-MODE_LIBRARY_ROUTINES"></span>マネージャーのユーザー モードのライブラリ ルーチンをフィルター処理します。

フィルター マネージャーは、ユーザー モード アプリケーションの読み込みとアンロード ミニフィルター ドライバーを使用するための次サポート ルーチンを提供します。

[**FilterLoad**](https://msdn.microsoft.com/library/windows/hardware/ff541504)

[**FilterUnload**](https://msdn.microsoft.com/library/windows/hardware/ff541516)

作成とミニフィルター ドライバーおよびインスタンスのハンドルを閉じるには、次のサポート ルーチンが用意されています。

[**FilterClose**](https://msdn.microsoft.com/library/windows/hardware/ff540453)

[**節**](https://msdn.microsoft.com/library/windows/hardware/ff540467)

[**FilterInstanceClose**](https://msdn.microsoft.com/library/windows/hardware/ff540524)

[**FilterInstanceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff540528)

アタッチとデタッチ ミニフィルター ドライバーのインスタンスには、次のサポート ルーチンが用意されています。

[**FilterAttach**](https://msdn.microsoft.com/library/windows/hardware/ff540442)

[**FilterAttachAtAltitude**](https://msdn.microsoft.com/library/windows/hardware/ff540448)

[**FilterDetach**](https://msdn.microsoft.com/library/windows/hardware/ff540475)

次のサポート ルーチンは、フィルター、ボリューム、およびインスタンスを列挙するために用意されています。

[**FilterFindFirst**](https://msdn.microsoft.com/library/windows/hardware/ff540485)

[**FilterFindNext**](https://msdn.microsoft.com/library/windows/hardware/ff540488)

[**FilterInstanceFindFirst**](https://msdn.microsoft.com/library/windows/hardware/ff540541)

[**FilterInstanceFindNext**](https://msdn.microsoft.com/library/windows/hardware/ff541493)

[**FilterVolumeFindFirst**](https://msdn.microsoft.com/library/windows/hardware/ff541525)

[**FilterVolumeFindNext**](https://msdn.microsoft.com/library/windows/hardware/ff541530)

[**FilterVolumeInstanceFindFirst**](https://msdn.microsoft.com/library/windows/hardware/ff541541)

[**FilterVolumeInstanceFindNext**](https://msdn.microsoft.com/library/windows/hardware/ff541551)

情報の照会には、次のサポート ルーチンが用意されています。

[**FilterGetDosName**](https://msdn.microsoft.com/library/windows/hardware/ff540492)

[**FilterGetInformation**](https://msdn.microsoft.com/library/windows/hardware/ff540500)

[**FilterInstanceGetInformation**](https://msdn.microsoft.com/library/windows/hardware/ff541499)

ユーザー操作によって開始された通信には、次のサポート ルーチンが用意されています。

[**FilterConnectCommunicationPort**](https://msdn.microsoft.com/library/windows/hardware/ff540460)

[**FilterSendMessage**](https://msdn.microsoft.com/library/windows/hardware/ff541513)

ミニフィルター ドライバーによって開始された通信に応答するは、次のサポート ルーチンが用意されています。

[**FilterGetMessage**](https://msdn.microsoft.com/library/windows/hardware/ff540506)

[**FilterReplyMessage**](https://msdn.microsoft.com/library/windows/hardware/ff541508)

 

 




