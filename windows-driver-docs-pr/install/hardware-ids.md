---
title: Hardware ID (ハードウェア ID)
description: ハードウェア ID は、デバイスを INF ファイルに一致させるために Windows が使用するベンダー定義の識別文字列です。
ms.assetid: 9eb894d6-4e83-4c08-8165-f30d6636da75
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 06787d3c9d10fcfc0558aafa272104672b217c13
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007623"
---
# <a name="hardware-id"></a>Hardware ID (ハードウェア ID)


ハードウェア ID は、デバイスを INF ファイルに一致させるために Windows が使用するベンダー定義の識別文字列です。 ほとんどの場合、デバイスにはハードウェア ID の一覧が関連付けられています。 (ただし、例外があります。1394デバイスの識別子は、デバイスのハードウェア Id の一覧を報告します。ハードウェア Id は、適合性が高い順に一覧表示する必要があります。




ハードウェア ID には、次のいずれかの汎用形式があります。

`<enumerator>\\<enumerator-specific-device-ID>`

これは、1つの列挙子によってプラグアンドプレイ (PnP) マネージャーに報告された個々の PnP デバイスに対して最も一般的な形式です。 新しい列挙子は、次の形式または次の形式を使用する必要があります。 列挙子固有のデバイス Id の詳細については、「[デバイス識別子の形式](device-identifier-formats.md)」を参照してください。

`\*<generic-device-ID>`

アスタリスクは、デバイスが1つ以上の列挙子 (ISAPNP や BIOS など) によってサポートされていることを示します。 この種類の ID の詳細については、「[ジェネリック識別子](generic-identifiers.md)」を参照してください。

`<device-class-specific-ID>`

## <a name="selecting-a-hardware-id"></a>ハードウェア ID の選択

@No__t-0 などの汎用名前空間を共有するルート列挙デバイスでは、OS のアップグレード時にデバイスマネージャーで競合が発生する可能性があります。

これを回避するには、ルートで列挙されたデバイスを含むドライバーごとに一意の名前空間を使用します。 USB またはシステムデバイスの場合は、`ROOT\USB` または `ROOT\SYSTEM”` を使用するのではなく、`ROOT\[COMPANYNAME]\[DEVICENAME]` を使用します。  また、ドライバーインストーラーのコードでは、devnode が既に存在するかどうかを確認し、をインストールする前に必要な修正措置をとる必要があります。

独自の名前付け規則を確立した既存のデバイスクラスは、カスタム形式を使用する場合があります。 ハードウェア ID 形式の詳細については、そのようなバスのハードウェア仕様を参照してください。 新しい列挙子は、この形式を使用できません。

ハードウェア ID の文字数 (NULL ターミネータを除く) は、MAX_DEVICE_ID_LEN よりも小さくする必要があります。 この制約は、すべてのフィールドの長さの合計と、ハードウェア ID の "\\" フィールド区切り記号に適用されます。 デバイス Id の制約の詳細については、「 [**IRP_MN_QUERY_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)」の「操作」セクションを参照してください。

## <a name="obtaining-the-list-of-hardware-ids-for-a-device"></a>デバイスのハードウェア Id の一覧を取得する

デバイスのハードウェア Id の一覧を取得するには、 *deviceproperty*パラメーターを**DevicePropertyHardwareID**に設定して[**iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)を呼び出します。 このルーチンが取得するハードウェア Id の一覧は、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)値です。 ハードウェアの一覧に含まれる最大文字数は、各ハードウェア ID と最後の NULL 終端文字の後の NULL 終端文字を含めて、REGSTR_VAL_MAX_HCID_LEN になります。 ハードウェア Id の一覧に表示される Id の最大数は64です。

## <a name="examples-of-hardware-ids"></a>ハードウェア Id の例

次の例では、最初の例が PnP デバイスの[汎用識別子](generic-identifiers.md)であり、2番目の例は[PCI デバイスの識別子](identifiers-for-pci-devices.md)です。

root @ no__t-0 @ no__t-1PNP0F08

PCI @ NO__T-0SUBSYS_00000000 & DEV_0001 & & REV_02





## <a name="see-also"></a>関連項目

[INF HardwareId ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-hardwareid-directive)


