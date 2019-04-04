---
title: COM ポートの外部の名前付け
description: COM ポートの外部の名前付け
ms.assetid: d517bc73-9687-45f8-a5f8-837ffe868fae
keywords:
- シリアル ドライバー WDK では、COM ポート
- COM ポートの WDK シリアル デバイス
- COM ポート、シリアル デバイス WDK
- WDL シリアル デバイスの名前
- 外部の名前付けの WDK シリアル デバイス
- シンボリック リンク WDK シリアル デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e55032761d413e3d12eb4d5ab5c0cb4c99023189
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578723"
---
# <a name="external-naming-of-com-ports"></a>COM ポートの外部の名前付け





既定では、シリアル関数ドライバーは、シリアル ポートのシンボリック リンクの名前を作成し、GUID を登録します\_DEVINTERFACE\_com ポート*デバイス インターフェイス*ポート。 シリアル ポートは、定義上、 [COM ポート](configuration-of-com-ports.md)関連付けられている、COM ポートのデバイスのインターフェイスを持つ場合にのみです。

プラグ アンド プレイ シリアル デバイスでは、外部の名前付けによって制御されます、 **SerialSkipExternalNaming**デバイスのハードウェア キーの下のエントリの値。 場合、 **SerialSkipExternalNaming**エントリの値が存在しないか、その値がゼロ、シリアルが COM ポートのデバイスのインターフェイスを作成します。 それ以外の場合、シリアルが COM ポートのインターフェイスを作成できません。 シリアルでは、従来の COM ポートのこのエントリの値をサポートしていませんし、常に、従来の COM ポートの COM ポート デバイス インターフェイスを作成します。

シリアルでは、COM ポートのデバイスのインターフェイスを作成する次のタスクを実行します。

- 間にシンボリック リンクを作成します。  **\\\dosdevices\z\\**&lt;*PortName* &gt;と COM ポートの内部デバイス オブジェクトの名前。

  &lt;*PortName* &gt;の値である、 **PortName** (または**識別子**) COM ポートのエントリの値。 ポート クラス インストーラー セット**PortName** com<em>&lt;n&gt;</em>ここで、 &lt; *n&gt;*  COM は、ポート番号をインストーラーを取得、 [COM ポート データベース](com-port-database.md)します。 シリアルは、ポートへのシンボリック リンクを作成するのにこの名前を使用します。 Windows をサポートする COM ポートの数に制限はありません。 ユーザー モードのクライアントでは、シンボリック リンクの名前を使用して、COM ポートを開きます。

- エントリの値を書き込み、 **\\レジストリ\\マシン\\ハードウェア\\DeviceMap\\SERIALCOMM**キー。

  エントリの値の名前は**\\デバイス\\シリアル**&lt;*m&gt;、* 場所*&lt;m&gt;* シリアルによってデバイスに割り当てられた番号です。 なお、デバイスのシリアル番号*&lt;m&gt;* not は、COM と同じポート番号 *&lt;n&gt;*。 値**\\デバイス\\シリアル**&lt;*m* &gt;の値に設定されている**PortName**します。

- GUID 型のデバイスのインターフェイスを登録\_DEVINTERFACE\_COM ポートの com ポート。

  クライアントは、COM ポート、インターフェイスの到着を通知に登録できます。 または登録されているすべての COM ポートのインターフェイスのシンボリック リンクの名前を取得することができます。

シリアルでレジストリ エントリの値を使用する方法の詳細については、[シリアルのレジストリ設定](registry-settings-for-serial.md)を参照してください。

 

 




