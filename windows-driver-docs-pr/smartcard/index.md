---
title: スマート カード リーダー デバイス設計ガイド
description: スマート カード リーダー デバイスのドライバーを開発するための設計ガイドです。
ms.assetid: e0827569-6c76-42a1-b94f-29235646519f
keywords:
- スマート カード ドライバー WDK
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
author: EliotSeattle
ms.openlocfilehash: e7ce1af5b932e117a1a1d81b0e333bf9ccd0b3f7
ms.sourcegitcommit: 85d02ecf7cbcfd802f41f68cea4cd4434284bdaa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68473545"
---
# <a name="smart-card-reader-devices-design-guide"></a>スマート カード リーダー デバイス設計ガイド

スマート カード リーダー デバイスのドライバーを開発するための設計ガイドです。

## <a name="in-this-section"></a>このセクションの内容

|トピック|説明|
|----|----|
|[スマート カード ドライバー環境](smart-card-driver-environment.md)|スマート カード リーダー ドライバーの標準環境について説明します。|
|[スマート カード リーダー ドライバーでの IOCTL 要求の管理](management-of-ioctl-requests-in-a-smart-card-reader-driver.md)|リーダー ドライバーが IOCTL 要求を管理する方法、コールバック ルーチン メカニズムの動作、およびリーダー ドライバーがコールバック ルーチンを初期化するために行う必要があることについて説明します。|
|[WDM リーダー ドライバー](wdm-reader-driver.md)|WDM リーダー ドライバーで必要とされるルーチンの一覧を示します。|
|[スマート カード ミニドライバー](smart-card-minidrivers.md)|スマート カード ミニドライバーは、カード ミニドライバーの開発者から複雑な暗号化操作の大部分をカプセル化することで、従来の暗号化サービス プロバイダー (CSP) の開発に対するより簡単な代替手段を提供します。|
|[スマート カード リーダーの状態](smart-card-reader-states.md)|スマート カード リーダーの状態とその意味を一覧表示しています。|
|[スマート カード リーダー ドライバーをインストールする](installing-smart-card-reader-drivers.md)|Windows 用のスマート カード リーダー ドライバーに固有のインストール情報を提供します。|
|[WDM スマート カード リーダー ドライバーを登録する](registering-a-wdm-smart-card-reader-driver.md)|WDM スマート カード リーダー ドライバーを登録するために必要なレジストリ値とその説明が提供されています。|
|[スマート カードのイベント ログをレジストリで有効にする](enabling-smart-card-event-logging-in-the-registry.md)|イベント ログのレジストリ値の名前とレジストリ値の内容。|
|[スマート カード リーダーの WDM デバイス名](wdm-device-names-for-smart-card-readers.md)|Windows オペレーティング システムでのデバイス名の名前付け規則に準拠するための手順です。|
|[スマート カード ドライバーのデバッグ](smart-card-driver-debugging.md)|スマート カード ドライバー ライブラリによるデバッグ機能のサポートについて説明します。|
|[仕様とリソース](specifications-and-resources.md)|Microsoft Windows オペレーティング システムでスマート カードのサポートを使用するには、「Interoperability Specification for ICCs and Personal Computer Systems (ICC およびパーソナル コンピューター システムの互換性の仕様)」に対応したスマート カード リーダーおよびカードが必要です。 また、スマート カード リーダーとデバイス ドライバーはプラグ アンド プレイに対応している必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 





