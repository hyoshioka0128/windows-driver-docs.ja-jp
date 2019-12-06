---
title: Bluetooth 無線のリセットと回復
description: Bluetooth ラジオの自動エラー復旧メカニズム
keywords:
- Bluetooth 無線エラー回復
- Bluetooth PLDR
ms.date: 09/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1def050b43664789bb89ba8e765e4371b959650f
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74860762"
---
# <a name="bluetooth-radio-reset-and-recovery"></a>Bluetooth 無線のリセットと回復

Bluetooth ラジオのリセットと回復は、Bluetooth ラジオ用の堅牢なリセットと復旧のメカニズムを導入する、Windows 10 バージョン1803以降のテクノロジです。 このメカニズムにより、Bluetooth ラジオは、誤動作、接続の切断、または操作コマンドへの無応答の原因となるハードウェア障害から回復できます。 目標は、無線を自動的に回復し、ユーザーエクスペリエンスをシームレスにし、システムの再起動が必要になる可能性を減らすことです。

Bluetooth ラジオのリセットと回復は、ファームウェアの依存関係の有無にかかわらず実装できます。 IHV または OEM パートナーは、サポートされているデバイスまたはファームウェアレベルのリセットメカニズムを使用して、すべての Windows Pc で利用可能なソフトウェアベースのリセットメカニズムを拡張し、回復が成功する可能性を高めることができます。

> [!IMPORTANT]
> **このトピックは、開発者を対象としています。** Bluetooth の問題が発生しているお客様の場合は、「 [Windows 10 での bluetooth の問題の修正](https://support.microsoft.com/help/14169/windows-10-fix-bluetooth-problems)」を参照してください。

## <a name="bluetooth-reset-and-recovery-scenarios"></a>Bluetooth のリセットと回復のシナリオ

Bluetooth のリセットと回復が開始される問題には、次の3つのカテゴリがあります。

- **バス列挙エラー:** このラジオは、基になるバス (Bluetooth の場合は通常、USB または UART) によってエラーが表示されます。これは、デバイスマネージャーの_表示エラー状態_(黄色の感嘆符) によって示されます。これは、基になるハードウェアエラーの兆候である可能性があります。

- **ドライバーの列挙エラー:** 基になるバスで列挙が成功_した_後、Bluetooth ラジオがエラー状態になります。 これは通常、オプションのドライバースタックを構築するときに発生します。たとえば、デバイスの Bluetooth ラジオデバイスノード (devnode) にフィルターまたは関数ドライバーがインストールされている場合です。 1つまたは複数の開始操作中にドライバーでエラーが発生し、その結果として PnP エラーが報告されると、エラーが発生する可能性があります。 このような操作の例として、デバイスへのファームウェアのダウンロードが挙げられます。

- **非列挙型エラー:** デバイスはエラー状態ではありませんが、それ以外の場合はドライバースタックに示されているように動作しません。 これらのエラーは列挙パスの外部で発生し、一般的に重大なトランスポート固有のエラーや、致命的なファームウェアエラーなどのデバイス固有の障害である可能性があります。 このような場合は、以下で説明する Bluetooth のリセットと復旧のメカニズムが使用されます。

## <a name="reset-and-recovery-mechanisms"></a>リセットと復旧のメカニズム

失敗した状態から回復するにはさまざまな方法がありますが、Bluetooth では、標準化された ACPI ベースの回復メカニズムを使用して、ラジオを正常な状態に復元しようとします。

[GUID_DEVICE_RESET_INTERFACE_STANDARD](https://docs.microsoft.com/windows-hardware/drivers/kernel/working-with-guid-device-reset-interface-standard)は、2つのレベルのリセットを定義します。 次の点に注意してください。

- リセットメカニズムは**内部デバイス**に対してのみ機能するため、ドングルなどの外部プラグ可能な Bluetooth ラジオはサポートされていません。

- リセットメカニズムでは、リセットを実際に実行するために、Windows (通常は関数ドライバースタック) と基になるファームウェア (通常は ACPI BIOS) の両方がサポートされている必要があります。

- 実際のリセットメカニズムはシステムに固有です。

| レベルのリセット | 実装 |
| --- | --- |
| 関数レベルのデバイスのリセット (FLDR) | リセット操作は特定のデバイスに制限され、他のデバイスからは表示されません。 再列挙がありません。 関数ドライバーは、操作後にハードウェアが元の状態に戻ったと想定する必要があります。  中間状態は保持されません。
| プラットフォームレベルのデバイスリセット (PLDR) | リセット操作は、特定のデバイスと、それに接続されている他のすべてのデバイスに、同じ電源レールまたはリセットラインを使用して影響を及ぼします。 リセット操作を実行すると、バスからデバイスが不足していると報告され、再列挙されます。 この種類のリセットは、リソースを共有するすべてのデバイスが元の状態に戻るため、システムに最も影響を与えます。|

- **FLDR をサポートするに**は、 [「ACPI ファームウェア: 関数レベルのリセット](https://docs.microsoft.com/windows-hardware/drivers/kernel/resetting-and-recovering-a-device#acpi-firmware-function-level-reset)」で詳しく説明されているように、__ADR_名前空間内で定義されている __RST メソッドが必要です。

- **PLDR をサポートするに**は、 [「ACPI ファームウェア: プラットフォームレベルのリセット](https://docs.microsoft.com/windows-hardware/drivers/kernel/resetting-and-recovering-a-device#acpi-firmware-platform-level-reset)」で詳しく説明されているように、__ADR_名前空間内で定義されている _RST または _PR3 メソッドが必要です。 __PR3_メソッドが使用されている場合、ACPI は D3Cold の電源サイクル機構を使用してリセットします。 これにより、デバイスから電力が削除され、その後復元されます。 他のデバイスが同じ電源レールを共有している場合は、そのデバイスもリセットされます。 __RST_メソッドが定義されていて、__PRR_ (powerresource) によって参照されている場合、その powerresource を使用するすべてのデバイスが影響を受けます。

  - PLDR は内部デバイスに対してのみ機能するため、ACPI のように宣言する必要があります。 USB デバイスの場合、内部で (ユーザーに表示されない) ポートを指定し、統合されたデバイスに接続できるようにするには、_ UPC を設定し_ます。PortIsConnectable_バイトを0xff と __pld にします。UserVisible_ビットを0にします。

  - PLDR に __PR3_ (D3Cold) メカニズムが使用されている場合は、systemwake や devicewake continue などのシナリオが動作することを確認します。 とは、D2 に対して適切な電源リソースが定義されていることを意味します。たとえば、__PR2_です。 次の表は、役に立つガイドです。

| 電源の状態 | ACPI リソース | 動作 |  
| --- | --- | --- |  
| D2 | _PR2 | クラスによって定義された、この状態の機能低下に必要なすべての電源またはクロック。 |  
| D3 ホット (reqd) | _PR2 | サポートされている次の上位の状態と同じリソース (D2、D1、または D0)。 |  
| D3cold | _PR3 | バス上にデバイスを表示し、バス固有のコマンドに応答するために必要な電源またはクロックのみ。|  

### <a name="related-links"></a>関連リンク

[デバイスのリセットと回復](https://docs.microsoft.com/windows-hardware/drivers/kernel/resetting-and-recovering-a-device)
