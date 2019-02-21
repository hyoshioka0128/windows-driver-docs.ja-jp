---
title: USBPRINT によって生成された識別子。SYS
description: USBPRINT によって生成された識別子。SYS
ms.assetid: 23f71429-7318-4442-81b8-3818298cfd16
keywords:
- USBPRINT します。SYS WDK デバイスのインストール
- 互換性のある Id WDK デバイスのインストール
- USB プリンター ドライバー WDK デバイスのインストール
- 印刷ドライバー WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51e3c0a7530bdc6f60e4ca9f23c6e579d1efda09
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535580"
---
# <a name="identifiers-generated-by-usbprintsys"></a>USBPRINT によって生成された識別子。SYS





オペレーティング システムはカーネル モード USB プリンター ドライバーを Windows 2000 以降、 *usbprint.sys* USB スタックにプリンターのサブシステムを接続します。 ネイティブの USB プリンター ドライバーでは、独自のカーネル モードの USB プリンター ドライバーの開発の必要性からベンダーを解放します。 これにより、高度なユーザー モードのプリンター ドライバーを開発するためにベンダは USB とパラレル プリンターの両方を操作します。

*Usbprint.inf*インストール ファイルには、すべての USB クラス 7 プリンター デバイスに一致する互換性のある ID が含まれています。 USB ハブのドライバーでは、これらのデバイスを列挙する場合、オペレーティング システムが見つかりますのハブのドライバーを生成する ID と一致する*usbprint.inf* 、USB プリンター ドライバーは読み込まと*usbprint.sys*します。 互換性のある ID で見つかった*usbprint.inf*は次の形式があります。

USB\\CLASS_07

各項目の意味は次のとおりです。

-   クラスの 07 h USB プリンター クラスに属しているデバイスを =

読み込まれるとすぐに、USB プリンター ドライバーはプリンター デバイスの新しい PDO を作成します。 USB プリンター ドライバーがによって生成される文字列識別子と互換性があるデバイスの IEEE 1284 文字列から派生した、新しいハードウェア ID を作成し、プラグ アンド プレイ (PnP) マネージャーは、新しく作成された PDO の識別文字列のクエリ、ときに、並列 bus 列挙子。 このハードウェア ID には、次の形式があります。

USBPRINT\\NameModel(20)Checksum(4)

各項目の意味は次のとおりです。

-   *NameModel(20)* が製造元の名前を連結したものと、最大 20 文字に切り捨てられます、デバイスのモデル。

-   *Checksum(4)* 製造元の名前およびモデル名から 4 文字の巡回冗長検査 (CRC) のコードが計算されます。

文字列内のスペースはアンダー スコアに置き換えられます。 たとえば、製造元の名前が"Hewlett-Packard"の場合は、モデル名が「HP 色 LaserJet 550」とチェックサム 3115、ハードウェア ID は次のようになります。

USBPRINT\\Hewlett-PackardHP_Co3115

前の例では、モデル名に"HP"と"Color"間のスペースが切り捨てられた型/モデルの文字列"Hewlett PackardHP_Co"を生成するために、アンダー スコアに置き換えられました。

**注**  オペレーティング システムによって生成される CRC 可能性がありますまたはその他の任意の CRC アルゴリズムによって、前のセクションで説明されているように計算された CRC に対応していません。 このため、プリンター ドライバーのプリンター ドライバーの INF ファイルを使用する正しい hardwareID を計算できませんしない場合があります。
HardwareID を取得するには、インストールされている USB プリンターに関連付けられている setupapi.dev.log ファイルを検索することをお勧めします。

 

 

 





