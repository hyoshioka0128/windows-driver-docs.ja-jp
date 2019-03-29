---
title: MB デバイス サービス
description: Windows 7 には、モバイル ブロード バンド (MB) デバイスをサポートするための NDIS (Network Device Interface Specification) ベースのドライバー モデルが導入されました。
ms.assetid: 7F9DFD96-2221-4F64-AC51-F336CCBED6BF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f9e1b26cf1dd3d64c901f5ad18eebc5a3755760
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578323"
---
# <a name="mb-device-services"></a>MB デバイス サービス


Windows 7 には、モバイル ブロード バンド (MB) デバイスをサポートするための NDIS (Network Device Interface Specification) ベースのドライバー モデルが導入されました。 Windows 8 では、USB ベース モバイル ブロード バンド デバイス用の標準化されたハードウェア インターフェイスを実装するためにモデルを展開します。 このハードウェア インターフェイス仕様は、モバイル ブロード バンド インターフェイス モデル (MBIM) と呼ばれます。

Windows 8 では、MBIM 仕様に準拠しているデバイスで動作するクラスが更新されたドライバーを提供します。 このモデルは、MB クラス ドライバーと呼ばれます。 ただし、クラス ドライバーをサポートできますありません MB のデバイスによって公開される機能のすべて。 IHV パートナーお客様はイノベーションに続行できるように、MB クラス ドライバーなどの提供、メカニズム、 [ **IMbnDeviceService インターフェイス**](https://msdn.microsoft.com/library/windows/desktop/hh780509)クラス ドライバーの動作を拡張する Ihv を許可するには機能。

**注**  MB デバイスのサービスを拡張する機能は、カーネル モード ドライバーの拡張子ではなく、ユーザー モード アプリケーションを使用して実現されます。

 

導入されたクラス ドライバーが Windows 7 機能制限付き MB デバイスの機能のサポートを備えた、USSD、EAP-SIM/別名および USB のセレクティブ中断、および拡張可能なデバイスの提供など、Windows 8 MB クラス ドライバーはその他の機能のネイティブ サポートを追加表示と制御のメカニズム。 [モバイル ブロード バンド WinRT API 概要](https://go.microsoft.com/fwlink/p/?linkid=242060)デバイス サービスを拡張する方法についていくつかの追加情報を提供します。

Windows 8 MB クラス ドライバーにより、垂直方向のソリューション プロバイダーを使用して、[モバイル ブロード バンド API インターフェイス](https://msdn.microsoft.com/library/windows/desktop/dd323268)されていない Windows によって提供される強化されたユーザー エクスペリエンスを作成します。 拡張メカニズムは、置き換えるには、MB クラス ドライバー自体でサポートされる機能が、強化する方法です。 たとえば、IHV は、デバイスでファームウェアの更新プログラムを実行するベンダー固有のソフトウェアを提供できます。 または、IHV が特定のベンダーに提供できるソフトウェアを提供する付加価値サービス SIM toolkit (STK) や電話帳など。 [AppContainer モバイル ブロード バンドの暗証番号 (pin)、接続および管理](https://go.microsoft.com/fwlink/p/?linkid=320381)にアクセスして、モバイル ブロード バンド機能を管理する AppContainer 内での Win32 と COM モバイル ブロード バンド Api を示します。

MB クラス ドライバーを拡張するためのメカニズムを提供するだけでなく ' の機能も用意されています Ihv 展開してインストールを有効にするためのメカニズムの Windows の付加価値ソフトウェアを介して Windows Update (WU)。

詳しくは、次のトピックをご覧ください。

-   「MBIM サービスと CID 拡張」セクション、[モバイル ブロード バンド インターフェイス モデル (MBIM) 仕様]( https://go.microsoft.com/fwlink/p/?linkid=320791)

 

 





