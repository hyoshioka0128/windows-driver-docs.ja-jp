---
title: Hardware ID (ハードウェア ID)
description: ハードウェア ID は、Windows を使用して、INF ファイルをデバイスに一致するベンダ定義の識別文字列です。
ms.assetid: 9eb894d6-4e83-4c08-8165-f30d6636da75
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c3a558ccf00d6db89267f473f647df1287bab04
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383823"
---
# <a name="hardware-id"></a>Hardware ID (ハードウェア ID)


ハードウェア ID は、Windows を使用して、INF ファイルをデバイスに一致するベンダ定義の識別文字列です。 ほとんどの場合、デバイスにはハードウェア ID の一覧が関連付けられています。 (ただしがあります: この例外は、1394 デバイス Id は、適合性が高い順に表示されるはずのハードウェア デバイスのハードウェア Id の一覧のレポートの識別子を参照してください。




ハードウェア ID では、次の一般的な形式のいずれかがあります。

`<enumerator>\\<enumerator-specific-device-ID>`

これは、プラグ アンド プレイ (PnP) manager を 1 つの列挙子によって報告された個々 の PnP デバイスの最も一般的な形式です。 新しい列挙子には、この形式または、次の形式を使用する必要があります。 列挙子に固有のデバイス Id の詳細については、次を参照してください。[デバイス識別子の書式設定](device-identifier-formats.md)します。

`\*<generic-device-ID>`

アスタリスクでは、デバイスが ISAPNP と BIOS などの 1 つ以上の列挙子によってサポートされていることを示します。 この種類の ID の詳細については、次を参照してください。[ジェネリック識別子](generic-identifiers.md)します。

`<device-class-specific-ID>`

## <a name="selecting-a-hardware-id"></a>ハードウェア ID の選択

ルートが汎用的な名前空間を共有するデバイスを列挙`ROOT\SYSTEM`可能性がありますの競合が発生して OS のアップグレード時にデバイス マネージャーで黄色の感嘆符します。

これを回避するには、ルート列挙されたデバイスを含むドライバーごとに一意の名前空間を使用します。 使用する代わりに、USB またはシステム デバイスの`ROOT\USB`または`ROOT\SYSTEM”`使用`ROOT\[COMPANYNAME]\[DEVICENAME]`します。  さらに、ドライバーのインストーラーのコードは devnode が既に存在するかどうかを確認し、インストールする前に、必要な措置を実行する必要があります。

確立されている独自の名前付け規則、既存のデバイス クラスには、カスタムの形式を使用します。 ハードウェア ID の形式については、このようなバスのハードウェア仕様を参照してください。 新しい列挙子では、この形式は使用しないでください。

文字、終端の NULL を除く、ハードウェア ID の数は、MAX_DEVICE_ID_LEN 未満である必要があります。 この制約が適用されるすべてのフィールドと任意の長さの合計"\\"フィールドの区切りには、ハードウェア ID デバイス Id の制約の詳細については、の操作」セクションを参照してください。 [ **IRP_MN_QUERY_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)します。

## <a name="obtaining-the-list-of-hardware-ids-for-a-device"></a>デバイスのハードウェア Id の一覧を取得します。

デバイスのハードウェア Id の一覧を取得するには、呼び出す[ **IoGetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)で、 *DeviceProperty*パラメーターに設定**DevicePropertyHardwareID**. このルーチンを取得するハードウェア Id の一覧は、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)値。 各ハードウェア ID と最終的な NULL 終端文字の後に、NULL 終端文字を含む、ハードウェア一覧内の文字の最大数は、REGSTR_VAL_MAX_HCID_LEN です。 ハードウェア Id の一覧で、Id の考えられる最大数は、64 です。

## <a name="examples-of-hardware-ids"></a>ハードウェア Id の例

最初の例には、次に、[汎用識別子](generic-identifiers.md)PnP デバイス、および 2 つ目の例は、 [PCI デバイスの識別子](identifiers-for-pci-devices.md):

ルート\\\*PNP0F08

PCI\\VEN_1000 &AMP; DEV_0001 &AMP; SUBSYS_00000000 REV_02





## <a name="see-also"></a>関連項目

[INF HardwareId ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-hardwareid-directive)


