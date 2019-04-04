---
title: レジストリ キーのオブジェクト
description: レジストリ キーのオブジェクト
ms.assetid: c666f0cc-5a8a-4df8-9c65-08e3b044a08f
keywords:
- ヘルパーは、WDK オーディオ、レジストリ キー オブジェクトをオブジェクトします。
- レジストリ キー オブジェクトの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5ccf39d2ffe1144021ab90a83821717a925ec6d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581659"
---
# <a name="registry-key-objects"></a>レジストリ キーのオブジェクト


## <span id="registry_key_objects"></span><span id="REGISTRY_KEY_OBJECTS"></span>


PortCls システム ドライバーの実装、 [IRegistryKey](https://msdn.microsoft.com/library/windows/hardware/ff536965)ミニポート ドライバーのためのインターフェイス。 IRegistryKey オブジェクトは、レジストリ キーを表します。 ミニポート ドライバーでは、レジストリ キー オブジェクトを使用して、次の操作します。

-   作成し、レジストリ キーの削除

-   レジストリ キーを列挙します。

-   クエリを実行し、レジストリ キーを設定

については、指定したキーの下のレジストリ エントリをレジストリ キー オブジェクトを照会するときに、クエリは異なるキー クエリ構造体を使用してそれぞれの 3 つの形式のいずれかの情報を出力できます。 次の表は、 [**キー\_情報\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff553373)の 3 つのキー クエリの構造を示す列挙値は、クエリによって出力します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KEY_INFORMATION_CLASS 値</th>
<th align="left">キー クエリ構造</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>KeyBasicInformation</strong></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553355" data-raw-source="[&lt;strong&gt;KEY_BASIC_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553355)"><strong>KEY_BASIC_INFORMATION</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>KeyFullInformation</strong></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553367" data-raw-source="[&lt;strong&gt;KEY_FULL_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553367)"><strong>KEY_FULL_INFORMATION</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>KeyNodeInformation</strong></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553392" data-raw-source="[&lt;strong&gt;KEY_NODE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553392)"><strong>KEY_NODE_INFORMATION</strong></a></p></td>
</tr>
</tbody>
</table>

 

既存のレジストリ キーを開くか、新しいレジストリ キーの作成、アダプタのドライバを呼び出すことができます、 [ **PcNewRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff537716)関数、およびミニポート ドライバーには、ポート ドライバーを呼び出すことができます[ **IPort::NewRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff536945)メソッド。 2 つの呼び出しは似ていますが、 **PcNewRegistryKey**関数には、2 つのパラメーターの追加が必要な*デバイス オブジェクト*と*サブデバイス*。 詳細については、**PcNewRegistryKey**を参照してください。

ミニポート ドライバーが新しいを作成します[IRegistryKey](https://msdn.microsoft.com/library/windows/hardware/ff536965)オブジェクト、オブジェクトは、既存のサブキーを開きますかが存在しない場合は、新しいレジストリ サブキーを作成します。 どちらの場合は、レジストリ キー オブジェクトは、キーを識別するハンドルを格納します。 そのオブジェクトが後で解放されるときに、その参照カウントをデクリメントを 0 に、オブジェクトは、キーへのハンドルを自動的に閉じます。

[IRegistryKey](https://msdn.microsoft.com/library/windows/hardware/ff536965)インターフェイスは、次のメソッドをサポートしています。

[**IRegistryKey::DeleteKey**](https://msdn.microsoft.com/library/windows/hardware/ff536967)

[**IRegistryKey::EnumerateKey**](https://msdn.microsoft.com/library/windows/hardware/ff536968)

[**IRegistryKey::EnumerateValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff536969)

[**IRegistryKey::NewSubKey**](https://msdn.microsoft.com/library/windows/hardware/ff536970)

[**IRegistryKey::QueryKey**](https://msdn.microsoft.com/library/windows/hardware/ff536971)

[**IRegistryKey::QueryRegistryValues**](https://msdn.microsoft.com/library/windows/hardware/ff536972)

[**IRegistryKey::QueryValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff536973)

[**IRegistryKey::SetValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff536975)

 

 




