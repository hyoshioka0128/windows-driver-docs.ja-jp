---
title: Hardware ID (ハードウェア ID)
description: ハードウェア ID は、デバイスを INF ファイルと対応付けるために Windows で使用されるベンダー定義の識別文字列です。
ms.assetid: 9eb894d6-4e83-4c08-8165-f30d6636da75
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: cd75a09e4dc79c36d9abfc75f02d8238a5a98447
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828816"
---
# <a name="hardware-id"></a>Hardware ID (ハードウェア ID)


ハードウェア ID は、デバイスを INF ファイルと対応付けるために Windows で使用されるベンダー定義の識別文字列です。 ほとんどの場合、デバイスにはハードウェア ID の一覧が関連付けられています。 (ただし、例外があります。1394 の識別子を参照してください。デバイスからは、デバイスのハードウェア ID の一覧が報告されます。このハードウェア ID は、適合性が高い値から順に一覧表示されます。




ハードウェア ID には、次のいずれかの一般的な形式があります。

`<enumerator>\\<enumerator-specific-device-ID>`

これは、1 つの列挙子でプラグ アンド プレイ (PnP) マネージャーに報告される個々の PnP デバイスの最も一般的な形式です。 新しい列挙子には、この形式または次の形式を使用する必要があります。 列挙子固有のデバイス ID の詳細については、「[デバイス識別子の形式](device-identifier-formats.md)」を参照してください。

`\*<generic-device-ID>`

アスタリスクは、デバイスが複数の列挙子 (ISAPNP や BIOS など) によってサポートされていることを示します。 この種類の ID の詳細については、「[汎用識別子](generic-identifiers.md)」を参照してください。

`<device-class-specific-ID>`

## <a name="selecting-a-hardware-id"></a>ハードウェア ID の選択

`ROOT\SYSTEM` などの一般的な名前空間を共有するルート列挙デバイスは、OS のアップグレード時にデバイス マネージャーで競合と黄色の感嘆符の表示が発生する可能性があります。

これを回避するには、ルート列挙デバイスを含む各ドライバーに一意の名前空間を使用します。 USB またはシステム デバイスの場合は、`ROOT\USB` または `ROOT\SYSTEM”` を使用する代わりに `ROOT\[COMPANYNAME]\[DEVICENAME]` を使用します。  また、ドライバー インストーラーのコードでは、devnode が既に存在するかどうかを確認し、インストール前に必要な修正措置を取る必要があります。

独自の名前付け規則が確立している既存のデバイス クラスの場合、カスタムの形式が使用されることがあります。 ハードウェア ID の形式の詳細については、そのようなバスのハードウェア仕様を参照してください。 新しい列挙子には、このような形式を使用しないでください。

NULL ターミネーターを除くハードウェア ID の文字数は、MAX_DEVICE_ID_LEN 未満にする必要があります。 この制約は、ハードウェア ID 内のすべてのフィールドの長さと "\\" フィールド区切り記号の合計に適用されます。 デバイス ID の制約の詳細については、「[**IRP_MN_QUERY_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)」の「操作」セクションを参照してください。

## <a name="obtaining-the-list-of-hardware-ids-for-a-device"></a>デバイスのハードウェア ID の一覧を取得する

デバイスのハードウェア ID の一覧を取得するには、*DeviceProperty* パラメーターを **DevicePropertyHardwareID** に設定して [**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty) を呼び出します。 このルーチンが取得するハードウェア ID の一覧は [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) 値です。 ハードウェア一覧の最大文字数は、各ハードウェア ID の後の NULL 終端文字と最後の NULL 終端文字を含め、REGSTR_VAL_MAX_HCID_LEN です。 ハードウェア ID の一覧に表示される ID の最大数は 64 です。

## <a name="examples-of-hardware-ids"></a>ハードウェア ID の例

以下の中で、最初の例は PnP デバイスの[汎用識別子](generic-identifiers.md)であり、2 つ目の例は [PCI デバイスの識別子](identifiers-for-pci-devices.md)です。

root\\\*PNP0F08

PCI\\VEN_1000&DEV_0001&SUBSYS_00000000&REV_02





## <a name="see-also"></a>参照

[INF HardwareId ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-hardwareid-directive)


