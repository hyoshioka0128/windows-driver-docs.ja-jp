---
title: OEMForceFeedback レジストリ設定
description: OEMForceFeedback レジストリ設定
ms.assetid: c29fe1e8-1cd9-4b32-96d7-1afae5a49d42
keywords:
- 強制的に WDK を非表示に OEMForceFeedback settiings フィードバック ドライバー
- WDK の HID OEMForceFeedback キー
- レジストリ WDK フォース フィードバック
- 効果サブキー WDK フォース フィードバック
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cd068521e1b0eecbf9c1518515808374f10d4fe6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381053"
---
# <a name="oemforcefeedback-registry-settings"></a>OEMForceFeedback レジストリ設定





ジョイスティックの新しいレジストリ エントリは、OEM 固有のキーがインストールされている各ジョイスティック デバイスの種類のレジストリ パスにキーの下の下にあります**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\MediaProperties\\PrivateProperties\\ジョイスティック\\OEM**します。 デバイスが最初にインストールしと参照の目的でのみ使用し、この OEM 固有のキーの下に格納されたデータが初期化されます。 ジョイスティックの既存のデバイスに対して定義されている値、2 つの新しい省略可能な汎用値および強制の一連のほか、フィードバックの特定の値が定義されています。

2 つの一般的な値は、バージョン情報を含むバイナリ値と**製造元**文字列値 (REGSTR\_VAL\_regstr.h の製造元) 製造元の名前の文字列を格納します。 既存の後者は、補完**OEMName**をデバイスの名前を保持する値。

新しい**OEMForceFeedback**フォース フィードバックの特定のキーと値を保持するためにキーが定義されています。 このキーの下では、**効果**ごとの 2 つの値を格納しているサブキー。

で、**効果**サブキーが各効果の 1 つのサブキーの一覧を示します。 各サブキーの名前は、フォームのグローバル一意識別子 (GUID)"{12345678-1234-1234-1234-123456789012}"。 「{...}」をという名前のキーの下にあります。 2 つの値です。 既定値は、結果の文字列のフレンドリ名です。 **属性**値は、 [ **DIEFFECTATTRIBUTES** ](https://docs.microsoft.com/windows/desktop/api/dinputd/ns-dinputd-dieffectattributes)構造体。

```cpp
"{guid1}"
    Default value = friendly name for effect {guid1} (string)
    "Attributes" = DIEFFECTATTRIBUTES structure (binary)
"{guid2}"
    Default value = friendly name for effect {guid2} (string)
    "Attributes" = DIEFFECTATTRIBUTES structure (binary)
```

**OEMForceFeedback**キーには、デバイスの属性は、2 つの省略可能な値のいずれかを格納している値も含まれています。 オプションの値の使用**CLSID**リング 3 ドライバー (DLL) を使用する場合と**VJoyD** ring 0 ドライバー (VxD) を使用している場合。

```cpp
"Attributes" = DIFFDEVICEATTRIBUTES structure (binary)
"CLSID" = {GUID} for force feedback effect driver (string)(optional)
"VJoyD" = zero-length binary (optional)
```

省略可能な値の名前を示すインターフェイスの形式が使用されます。 場合、 **CLSID**値が存在する必要があります形式で GUID を含む文字列値を"{12345678-1234-1234-1234-123456789012}"ドライバー インターフェイスを提供する COM オブジェクト。 場合、 **VJoyD**値が存在するを使用するデバイスに関連付けられている VJoyD ミニドライバーの余分なコールバック ドライバー インターフェイスを指定する必要があることを示す、長さ 0 のバイナリ値になります。 値は、実装されると、ヒューマン インターフェイス デバイス (HID) はドライバー インターフェイスを提供します。 を示すために追加されます。

デバイスは、定義済みのカテゴリのいずれにも該当しないハードウェアの効果をサポートしている場合 (DIEFT\_CONSTANTFORCE、DIEFT\_RAMPFORCE、DIEFT\_定期的、DIEFT\_条件、または DIEFT\_CUSTOMFORCE)、次に、 [ **DIEFFECTATTRIBUTES** ](https://docs.microsoft.com/windows/desktop/api/dinputd/ns-dinputd-dieffectattributes)効果 DIEFT を指定する必要があります構造体\_エフェクトの種類とハードウェア。

デバイスが (前の段落に記載) 定義済みのカテゴリのいずれかに該当するハードウェアの効果をサポートしてが (DICONSTANTFORCE、DIRAMPFORCE、標準の種類に固有のデータ構造の一部ではない追加のパラメーターを受け取りますDIPERIODIC、DICONDITION、または DICUSTOMFORCE) これらの構造については、DirectInput のセクションの DirectX ソフトウェア開発キット (SDK) を参照してください。 このような場合は、次のように、効果が表示されます。

-   定義済みのカテゴリ で効果を一覧表示します。 アプリケーションでは、定義済みのカテゴリで、効果を作成する場合、ドライバーは、標準の種類に固有のデータ構造の一部ではない、指定されたパラメーターの適切な既定値を提供する必要があります。

-   DIEFT で効果を一覧表示\_ハードウェア カテゴリ。 特殊な種類に固有余分なパラメーターを格納する構造 (DIPERIODICFORCEWITHDECAY) などを作成します。

この方法で、ハードウェア用に設計されたアプリケーションことができますを使用して、効果の 2 つ目の記述子、効果のすべての機能にアクセスする汎用ハードウェア用に設計されたアプリケーションの基本的な機能にアクセスする最初の効果の記述子を使用できますが、効果です。

 

 




