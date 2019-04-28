---
title: Hardware ID (ハードウェア ID)
description: ハードウェア ID は、Windows を使用して、INF ファイルをデバイスに一致するベンダ定義の識別文字列です。
ms.assetid: 9eb894d6-4e83-4c08-8165-f30d6636da75
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee6ed3809fd262637b30b31b515bc9d06457b804
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360604"
---
# <a name="hardware-id"></a>Hardware ID (ハードウェア ID)


ハードウェア ID は、Windows を使用して、INF ファイルをデバイスに一致するベンダ定義の識別文字列です。 ほとんどの場合、デバイスにはハードウェア ID の一覧が関連付けられています。 (ただしがあります: この例外は、1394 デバイス Id は、適合性が高い順に表示されるはずのハードウェア デバイスのハードウェア Id の一覧のレポートの識別子を参照してください。




ハードウェア ID では、次の一般的な形式のいずれかがあります。

<a href="" id="-enumerator---enumerator-specific-device-id-"></a>*&lt;列挙子&gt;\\&lt;列挙子特定のデバイス ID&gt;*  
これは、プラグ アンド プレイ (PnP) manager を 1 つの列挙子によって報告された個々 の PnP デバイスの最も一般的な形式です。 新しい列挙子には、この形式または、次の形式を使用する必要があります。 列挙子に固有のデバイス Id の詳細については、次を参照してください。[デバイス識別子の書式設定](device-identifier-formats.md)します。

<a href="" id="--generic-device-id-"></a>*\*&lt;generic-device-ID&gt;*  
アスタリスクでは、デバイスが ISAPNP と BIOS などの 1 つ以上の列挙子によってサポートされていることを示します。 この種類の ID の詳細については、次を参照してください。[ジェネリック識別子](generic-identifiers.md)します。

<a href="" id="-device-class-specific-id-"></a>*&lt;デバイス クラス固有 ID&gt;*  
確立されている独自の名前付け規則、既存のデバイス クラスには、カスタムの形式を使用します。 ハードウェア ID の形式については、このようなバスのハードウェア仕様を参照してください。 新しい列挙子では、この形式は使用しないでください。

文字、終端の NULL を除く、ハードウェア ID の数は、MAX_DEVICE_ID_LEN 未満である必要があります。 この制約が適用されるすべてのフィールドと任意の長さの合計"\\"フィールドの区切りには、ハードウェア ID デバイス Id の制約の詳細については、の操作」セクションを参照してください。 [ **IRP_MN_QUERY_ID**](https://msdn.microsoft.com/library/windows/hardware/ff551679)します。

デバイスのハードウェア Id の一覧を取得するには、呼び出す[ **IoGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff549203)で、 *DeviceProperty*パラメーターに設定**DevicePropertyHardwareID**. このルーチンを取得するハードウェア Id の一覧は、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)値。 各ハードウェア ID と最終的な NULL 終端文字の後に、NULL 終端文字を含む、ハードウェア一覧内の文字の最大数は、REGSTR_VAL_MAX_HCID_LEN です。 ハードウェア Id の一覧で、Id の考えられる最大数は、64 です。

### <a name="examples-of-hardware-ids"></a>ハードウェア Id の例

最初の例には、次に、[汎用識別子](generic-identifiers.md)PnP デバイス、および 2 つ目の例は、 [PCI デバイスの識別子](identifiers-for-pci-devices.md):

ルート\\\*PNP0F08

PCI\\VEN_1000 &AMP; DEV_0001 &AMP; SUBSYS_00000000 REV_02

 

 





