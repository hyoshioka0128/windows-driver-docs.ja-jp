---
title: システム用に予約されているシステム定義のデバイス セットアップ クラス
description: システム用に予約されているシステム定義のデバイス セットアップ クラス
ms.assetid: 519a8833-8ed0-40c8-b7cb-a86f13191227
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e43522a6366e6e5bde454e778e371b6dc14fc48f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580372"
---
# <a name="system-defined-device-setup-classes-reserved-for-system-use"></a>システム用に予約されているシステム定義のデバイス セットアップ クラス


次のクラスと Guid は適していないデバイス (またはドライバー) をインストールする Windows 2000 または Windows の以降のバージョン。

**アダプター**<br/>
クラス アダプターを =<br/>
ClassGuid = {4d36e964-e325-11ce-bfc1-08002be10318}<br/>
このクラスは廃止されています。

**APM**<br/>
クラス APMSupport を =<br/>
ClassGuid = {d45b1c18-c8fa-11d1-9f77-0000f805f530}<br/>
このクラスは、システムの使用に予約されています。

<a href="" id="computer-"></a>**コンピューター**<br/>
クラスのコンピューターを =<br/>
ClassGuid = {4d36e966-e325-11ce-bfc1-08002be10318}<br/>
このクラスは、システムの使用に予約されています。

<a href="" id="decoders-"></a>**デコーダー**<br/>
クラス デコーダーを =<br/>
ClassGuid = {6bdd1fc2-810f-11d0-bec7-08002be2092f}<br/>
このクラスは、将来使用するために予約されています。

**ホスト側の IEEE 1394 カーネル デバッガーのサポート**<br/>
クラス 1394Debug を =<br/>
ClassGuid = {66f250d6-7801-4a64-b139-eea80a450b24}<br/>
このクラスは、システムの使用に予約されています。

**IEEE 1394 IP ネットワークの列挙子**<br/>
クラス Enum1394 を =<br/>
ClassGuid = {c459df55-db08-11d1-b009-00a0c9081ff6}<br/>
このクラスは、システムの使用に予約されています。

**ないドライバー**<br/>
クラス NoDriver を =<br/>
ClassGuid = {4d36e976-e325-11ce-bfc1-08002be10318}<br/>
このクラスは廃止されています。

<a href="" id="non-plug-and-play-drivers-"></a>**プラグ アンド プレイ ドライバー**<br/>
クラス LegacyDriver を =<br/>
ClassGuid = {8ecc055d-047f-11d1-a537-0000f8753ed1}<br/>
このクラスは、システムの使用に予約されています。

<a href="" id="other-devices-"></a>**その他のデバイス**<br/>
クラス = Unknown<br/>
ClassGuid = {4d36e97e-e325-11ce-bfc1-08002be10318}<br/>
このクラスは、システムの使用に予約されています。 型が、システムを判断することはできません、列挙されたデバイスは、このクラスの下にインストールされます。 ないこのクラスを使用かわからない場合、デバイスが属するクラスでします。 正しいデバイス セットアップ クラスを判別するか、新しいクラスを作成します。

<a href="" id="printer-upgrade-"></a>**プリンターのアップグレード**<br/>
クラス PrinterUpgrade を =<br/>
ClassGuid = {4d36e97a-e325-11ce-bfc1-08002be10318}<br/>
このクラスは、システムの使用に予約されています。

<a href="" id="sound-"></a>**サウンド**<br/>
クラスのサウンドを =<br/>
ClassGuid = {4d36e97c-e325-11ce-bfc1-08002be10318}<br/>
このクラスは廃止されています。

**ストレージ ボリューム スナップショット**<br/>
クラス VolumeSnapshot を =<br/>
ClassGuid = {533c5b84-ec70-11d2-9505-00c04F79deaf}<br/>
このクラスは、システムの使用に予約されています。

**USB バス デバイス (ハブとホスト コント ローラー)**<br/>
クラス USB を =<br/>
ClassGuid = 36fc9e60-c465-11cf-8056-444553540000<br/>
このクラスには、USB ホスト コント ローラーと USB ハブはない USB 周辺機器が含まれます。 このクラスのドライバーは、システムが提供します。

 

 





