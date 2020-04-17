---
title: Windows でサポートされる HID クライアント
ms.assetid: E6584286-6BF1-40C7-83C1-D07077B13F3E
description: ''
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 262f2c06758841e92324e9d8b1a0cf15ceb3dcb4
ms.sourcegitcommit: ab45b5ee55705f88ac5f68ef4f45801c687279c1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81480744"
---
# <a name="hid-clients-supported-in-windows"></a>Windows でサポートされる HID クライアント


Windows では、次に示す最上位のコレクションがサポートされます。

| **[使用状況] ページ** | **使用状況** | **Windows 7** | **Windows 8** | **Windows 10** | **メモ** | **アクセスモード** |
| --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | 0x0001-0x0002 | はい | はい | はい | マウスクラスドライバーおよびマッパードライバー | ［排他］ |
| 0x0001 | 0x0004-0x0005 | はい | はい | はい | ゲームコントローラー | Shared |
| 0x0001 | 0x0006-0x0006 | はい | はい | はい | キーボード/キーパッドクラスドライバーとマッパードライバー | ［排他］ |
| 0x0001 | 0x000C | いいえ | はい | はい | フライトモードスイッチ | Shared |
| 0x0001 | 0x0080 | はい | はい | はい | システムコントロール (Power) | Shared |
| 0x000C | 0x0001 | はい | はい | はい (Windows 10 と Windows 10 Mobile の両方) | コンシューマーコントロール | 共有 (Windows 10 および Windows 10 Mobile の両方) |
| 0x000D | 0x0001 | はい | はい | はい | 外部ペンデバイス | ［排他］ |
| 0x000D | 0x0002 | はい | はい | はい | 統合されたペンデバイス | ［排他］ |
| 0x000D | 0x0004 | はい | はい | はい | Touchscreen | ［排他］ |
| 0x000D | 0x0005 | いいえ | はい | はい | 精度のタッチパッド (PTP) | ［排他］ |
| 0x0020 | \* 複数 | いいえ | はい | はい | センサー | Shared |
| 0x0084 | 0x004 | はい | はい | はい | HID UPS バッテリ | Shared |
| 0x008C | 0x0002 | いいえ | はい (Windows 8.1 以降) | はい | バーコードスキャナー (hidscanner .dll) | Shared |


上の表では、入力 HID クライアントのアクセスモードは、他の HID クライアントがその入力のターゲット受信者ではない場合に、グローバルな入力状態を受信または受信できないようにするためのものです。 そのため、セキュリティ上の理由により、このようなデバイスはすべて排他的に開かれます。 

共有モードでは、複数のアプリケーションからデバイスにアクセスできます。 たとえば、複数のアプリケーションがバーコードスキャナーにアクセスして、デバイスの機能を照会し、統計情報を取得することができます。 ただし、デコードされたデータをバーコードスキャナーから取得することは、排他モードで実行します。 使用法は、 [USB HID POS スキャナーの標準仕様](https://go.microsoft.com/fwlink/?linkid=830661)で定義されています。 

\* Multiple: 0x00 ~ 0xFF からのセンサーの使用は、さまざまな目的のためにセグメント化されています。 たとえば、0x10 は生体認証センサーを示します。0x40 は光センサーを示します。 これらの割り当ては連続していません。 センサーの使用状況の一覧については、「 [Review Request 39: HID Usage Table センサー Page](https://go.microsoft.com/fwlink/?linkid=830659)」を参照してください。 Windows でサポートされているセンサーの使用方法の詳細については、 [HID センサーの使用](https://go.microsoft.com/fwlink/?linkid=830658)方法に関する情報を参照してください。

 




