---
title: Windows 8 での WFP の変更
description: Windows 8 での WFP の変更
ms.assetid: B83EC5A5-6169-49AB-A7EC-F2078AA0735E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f1393411cc9f0d908d494ef03a4aee2b21297e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365702"
---
# <a name="wfp-changes-for-windows-8"></a>Windows 8 での WFP の変更


使用可能な関数と、Windows フィルタ リング プラットフォームを開始する Windows 8 での動作では、いくつかの変更が加えられました。 多くの場合、新しい機能を利用する必要がありますのコンパイル時またはを持つ、NTDDI コールアウト ドライバーを再コンパイル\_バージョン マクロ設定 NTDDI\_WIN8 します。

-   新機能:
    - [レイヤー 2 のフィルターを使用します。](using-layer-2-filtering.md)
    - [追跡プロキシの接続を使用します。](using-proxied-connections-tracking.md)
    - [仮想スイッチのフィルターを使用します。](using-virtual-switch-filtering.md)
-   新しい関数:
    - [**FwpsCalloutRegister2**](https://msdn.microsoft.com/library/windows/hardware/hh439576)
    - [**FwpsFlowAbort0**](https://msdn.microsoft.com/library/windows/hardware/hh439582)
    - [**FwpsInjectMacReceiveAsync0**](https://msdn.microsoft.com/library/windows/hardware/hh439588)
    - [**FwpsInjectMacSendAsync0**](https://msdn.microsoft.com/library/windows/hardware/hh439593)
    - [**FwpsNetBufferListAssociateContext1**](https://msdn.microsoft.com/library/windows/hardware/hh439674)
    - [**FwpsQueryConnectionRedirectState0**](https://msdn.microsoft.com/library/windows/hardware/hh439677)
    - [**FwpsRedirectHandleCreate0**](https://msdn.microsoft.com/library/windows/hardware/hh439681)
    - [**FwpsRedirectHandleDestroy0**](https://msdn.microsoft.com/library/windows/hardware/hh439684)
    - [**FwpsvSwitchEventsSubscribe0**](https://msdn.microsoft.com/library/windows/hardware/hh439687)
    - [**FwpsvSwitchEventsUnsubscribe0**](https://msdn.microsoft.com/library/windows/hardware/hh439691)
    - [**FwpsvSwitchNotifyComplete0**](https://msdn.microsoft.com/library/windows/hardware/hh439695)
-   新しいコールバック関数:
    - [*FWPS\_コールアウト\_分類\_FN2*](https://msdn.microsoft.com/library/windows/hardware/hh439337)
    - [*FWPS\_コールアウト\_通知\_FN2*](https://msdn.microsoft.com/library/windows/hardware/hh439963)
    - [*FWPS\_NET\_バッファー\_一覧\_通知\_FN1*](https://msdn.microsoft.com/library/windows/hardware/hh451260)
    - [*FWPS\_VSWITCH\_FILTER\_ENGINE\_REORDER\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451267)
    - [*FWPS\_VSWITCH\_インターフェイス\_イベント\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451269)
    - [*FWPS\_VSWITCH\_有効期間\_イベント\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451271)
    - [*FWPS\_VSWITCH\_ポリシー\_イベント\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451272)
    - [*FWPS\_VSWITCH\_ポート\_イベント\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451276)
    - [*FWPS\_VSWITCH\_ランタイム\_状態\_復元\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451281)
    - [*FWPS\_VSWITCH\_RUNTIME\_STATE\_SAVE\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451286)
-   新しい構造体。
    - [**FWPS\_FILTER2**](https://msdn.microsoft.com/library/windows/hardware/hh439768)
    - [**FWPS\_VSWITCH\_イベント\_ディスパッチ\_TABLE0**](https://msdn.microsoft.com/library/windows/hardware/hh451263)
-   新しい列挙体。
    - [**FWPS\_接続\_リダイレクト\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh439704)
    - [**FWPS\_フィールド\_エグレス\_VSWITCH\_イーサネット**](https://msdn.microsoft.com/library/windows/hardware/hh439709)
    - [**FWPS\_フィールド\_エグレス\_VSWITCH\_トランスポート\_V4**](https://msdn.microsoft.com/library/windows/hardware/hh439715)
    - [**FWPS\_FIELDS\_EGRESS\_VSWITCH\_TRANSPORT\_V6**](https://msdn.microsoft.com/library/windows/hardware/hh439721)
    - [**FWPS\_フィールド\_受信\_MAC\_フレーム\_ネイティブ**](https://msdn.microsoft.com/library/windows/hardware/hh439728)
    - [**FWPS\_フィールド\_イングレス\_VSWITCH\_イーサネット**](https://msdn.microsoft.com/library/windows/hardware/hh439733)
    - [**FWPS\_フィールド\_イングレス\_VSWITCH\_トランスポート\_V4**](https://msdn.microsoft.com/library/windows/hardware/hh439738)
    - [**FWPS\_FIELDS\_INGRESS\_VSWITCH\_TRANSPORT\_V6**](https://msdn.microsoft.com/library/windows/hardware/hh439745)
    - [**FWPS\_フィールド\_送信\_MAC\_フレーム\_ネイティブ**](https://msdn.microsoft.com/library/windows/hardware/hh439757)
    - [**FWPS\_VSWITCH\_イベント\_型**](https://msdn.microsoft.com/library/windows/hardware/hh451265)
-   列挙型の名前が変更されました。
    - [**FWPS\_フィールド\_受信\_MAC\_フレーム\_イーサネット**](https://msdn.microsoft.com/library/windows/hardware/ff551291) (が**FWPS\_フィールド\_受信\_MAC\_フレーム\_802\_3**)
    - [**FWPS\_フィールド\_送信\_MAC\_フレーム\_イーサネット**](https://msdn.microsoft.com/library/windows/hardware/ff551334) (が**FWPS\_フィールド\_送信\_MAC\_フレーム\_802\_3**)

 

 





