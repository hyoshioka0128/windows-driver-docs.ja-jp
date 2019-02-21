---
title: コントロールのミニドライバーのフロー
description: コントロールのミニドライバーのフロー
ms.assetid: c3c23d32-4023-445b-bd89-e0b454bec1ed
keywords:
- Stream.sys クラス ドライバー WDK Windows 2000 のカーネル、制御フロー
- ミニドライバー WDK Windows 2000 のカーネル、制御フローのストリーミング
- ミニドライバー WDK Windows 2000 カーネル ストリーミング、制御フロー
- ミニドライバー WDK ストリーミング ミニドライバーをストリーミングに初期化されていません。
- ストリーミング ミニドライバー WDK Windows 2000 のカーネルの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c24bb312c11716a9a4921190e919c4529c294575
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535792"
---
# <a name="minidriver-flow-of-control"></a>コントロールのミニドライバーのフロー





通常、次の一連の手順は初期化して、使用、および初期化解除ストリーミング ミニドライバーの後にします。 参照されている次のコマンドと構造体はこのドキュメントで他の場所で説明します。

**使用しての初期化中に、手順の後におよび初期化解除ストリーミング ミニドライバーは**

1.  プラグ アンド プレイの列挙子で、ミニドライバーでサポートされているハードウェア アダプターが検出されます。 列挙子は、シンボル参照の解決にレジストリを確認し、I/O サブシステムに要求を渡します。

2.  I/O サブシステムが、ミニドライバーを読み込みを呼び出すようにミニドライバーの**DriverEntry**ルーチン (を参照してください[ **Stream クラス ミニドライバーの DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff558717)) で、 [**HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff559682)構造に割り当てられ初期化します。 情報は、ファイル オブジェクトが作成された、 **DriverEntry**ルーチン。

3.  ミニドライバーの**DriverEntry**ルーチンを呼び出して、ストリーム クラス ドライバーの[ **StreamClassRegisterMinidriver** ](https://msdn.microsoft.com/library/windows/hardware/ff568263)関数とパス、 [ **HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff559682)をパラメーターとして構造体。 ハードウェア ベース\_初期化\_データ構造が処理される Srb ミニドライバー関数のアドレスが含まれています。 これにより、クラス ドライバーによって送信される Srb に応答するミニドライバーができます。

4.  初期化中に、ストリーム クラス ドライバーがで指定された関数を呼び出し、 [ **HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff559682)構造体の**HwReceivePacket**メンバー (を参照してください[ *StrMiniReceiveDevicePacket*](https://msdn.microsoft.com/library/windows/hardware/ff568463)) でとを SRB、**コマンド**メンバー SRB に設定\_初期化\_デバイス。 ミニドライバーは、ハードウェア アダプターを初期化します。

5.  ストリーム クラスのドライバーがで指定された関数を呼び出し、 [ **HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff559682)構造体の**HwReceivePacket**メンバーSRB の\_取得\_ストリーム\_情報。 ミニドライバーは、ストリームのサポートの詳細情報を返します。

6.  ストリーム クラスのドライバーがで指定された関数を呼び出し、 **HW\_初期化\_データ**構造体の**HwReceivePacket** SRB を持つメンバー\_を開く\_ストリームで、 [ **HW\_ストリーム\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff559697)構造体。 ミニドライバーは、指定されたストリームを開くために必要なハードウェア アクションを実行します。

7.  ストリーム クラス ドライバーを送信、SRB を渡すことによって、ストリームからデータを要求または\_読み取り\_データまたは SRB\_書き込み\_データ コマンドで指定された関数を**ReceiveDataPacket**ハードウェア ベースのメンバー\_ストリーム\_ストリームのオブジェクトの構造体。

8.  ストリーム クラス ドライバーを取得および適切なストリーム要求のブロックを渡すことによってプロパティと、ストリームの他のコントロールの情報を設定 ([**HW\_ストリーム\_要求\_ブロック** ](https://msdn.microsoft.com/library/windows/hardware/ff559702)) で指定された関数を**ReceiveControlPacket**ハードウェア ベースのメンバー\_ストリーム\_ストリームのオブジェクトの構造体。

9.  ストリーム クラスのドライバーがで指定された関数を呼び出すストリームを使用して、システムがある場合、 [ **HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff559682)構造体の**HwReceivePacket** SRB を持つメンバー\_閉じる\_ストリーム。 ミニドライバーは、指定されたストリームを閉じます。

10. アダプターの初期化を解除するときはと、ストリーム クラスのドライバーがで指定された関数を呼び出し、 [ **HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff559682)構造体の**HwReceivePacket** SRB を持つメンバー\_非\_デバイス。 ミニドライバーは、デバイスを消去します。

 

 




