---
title: デバイス管理用の名前空間オブジェクト
description: ACPI 5.0 仕様には、いくつかの種類のデバイスを管理するために使用する名前空間オブジェクトが定義されています。
ms.assetid: 26C3312D-B1B0-4843-BF4E-1B03630C0BDD
ms.date: 06/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: dc29478adbe553c1d9ab05456ebca8a6b0348eb5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364569"
---
# <a name="device-management-namespace-objects"></a>デバイス管理用の名前空間オブジェクト


[ACPI 5.0 仕様](https://uefi.org/specifications)いくつかの種類のデバイスを管理するために使用する名前空間オブジェクトを定義します。 たとえば、デバイスの id オブジェクトには、子デバイスのハードウェアの列挙をサポートしていない、I2C などのバスに接続するデバイスの id 情報が含まれます。 その他の種類の名前空間のオブジェクトでは、システム リソースを指定、デバイス依存関係を記述、およびデバイスを無効にすることができますを示すことができます。

## <a name="device-identification-in-windows"></a>Windows でのデバイスの識別


Windows のプラグ アンド プレイを検索して、デバイスの列挙子によって提供されるデバイスの識別子に基づいて、デバイス ドライバーを読み込みます。 列挙子は、デバイスから id 情報を抽出する方法を知っているバス ドライバーです。 (PCI、SD、および USB) などのいくつかのバスでは、この抽出を実行するハードウェアが定義したメカニズムがあります。 ありません (プロセッサ バスやシンプルな周辺機器のバス) バスを ACPI 名前空間で識別オブジェクトを定義します。

[ACPI の Windows ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)Acpi.sys、アセンブルでの非常に具体的には、デバイスを識別できるデバイスの識別子の文字列または非常に一般的には、ドライバーのニーズに応じてさまざまなこれらのオブジェクトで見つかった値。 ACPI 列挙のデバイスを識別するために作成された文字列パターンを次に示します。

```syntax
ACPI\VEN_vvv[v]&DEV_dddd&SUBSYS_sss[s]nnnn&REV_rrrr
ACPI\VEN_vvv[v]&DEV_dddd&SUBSYS_sss[s]nnnn
ACPI\VEN_vvv[v]&DEV_dddd&REV_rrrr
ACPI\VEN_vvv[v]&DEV_dddd
ACPI\vvv[v]dddd
```

デバイス マネージャーを開き、検査して、デバイスの Windows を作成するデバイスの id を確認できます、**ハードウェア Id**と**互換性 Id**列挙されたデバイスのプロパティ。 次の各文字列は、デバイスの読み込みにドライバーを識別するために、INF ファイルで指定する使用できます。 INF の照合順序が設定されて最も固有のハードウェア識別子 (ドライバーの最も優先度) から固有識別子 (最小限の推奨されるドライバー) に、デバイスの特定の機能について詳しく知るドライバーは、以下にあるものを置き換えることができます。特定 (およびそのため、デバイスの機能のサブセットのみをサポート)。

デバイスの id のみ、一致する INF を使用する必要がありますとことはありませんする解析か、デバイス ドライバーによって処理します。 デバイス ドライバーの読み込まれた特定のハードウェアを識別する必要がある場合は、適切なレジストリ キーをインストールするとき、INF ファイル セットことをお勧めします。 ドライバー、必要な情報を取得する初期化中にこれらのキーにアクセスできます。

## <a name="device-identification-in-acpi"></a>ACPI のデバイスの識別


### <a name="hardware-id-hid"></a>ハードウェア ID (\_HID)

ACPI のデバイスを特定するための最小要件は、ハードウェア ID (\_HID) オブジェクト。 \_HID の形式の文字列を返します"ABC\[D\]*xxxx*"ここで、"ABC\[D\]"("ベンダー ID")、デバイスの製造元を識別する 3 または 4 文字の文字列と*xxxx*仕入先 ("デバイス ID") によって製造された特定のデバイスを識別する 16 進の番号です。 ベンダー Id は、業界全体で一意である必要があります。 Microsoft では、これらの文字列が一意であることを確認するを割り当てます。 ベンダー Id から取得できます[プラグ アンド プレイ ID - PNPID 要求](https://go.microsoft.com/fwlink/p/?linkid=330999)します。

**注**  ACPI 5.0 は、ベンダーの PCI によって割り当てられた Id の使用もサポートしています。 \_HID と Microsoft のベンダー ID を取得する必要はありませんので、他の識別オブジェクト。 ハードウェアの id 要件の詳細については、6.1.5 を参照してください。"\_HID (ハードウェア ID)"、の、 [ACPI 5.0 仕様](https://uefi.org/specifications)します。



### <a name="compatible-id-cid"></a>互換性のある ID (\_CID)

Microsoft には、Windows に付属して受信トレイのドライバーと互換性のあるデバイスのベンダー ID"PNP"は予約されています。 Windows では、デバイスの Windows で提供されるドライバーの読み込みに使用できるこのベンダー ID を使用するためのデバイス id の数を定義します。 別のオブジェクトを互換性のある ID (\_CID) オブジェクト、これらの識別子を返すために使用します。 Windows は、ハードウェア Id を常に優先 (によって返される\_HID) 互換性 Id 経由で (によって返される\_CID) に一致して、ドライバーの INF の選択。 この設定により、ベンダー提供のデバイス固有ドライバーが利用できない場合、既定のドライバーとして扱う場合に、Windows で提供されるドライバーです。 次の表に、互換性 Id は、SoC プラットフォームで使用する新しく作成されます。

| 互換性 ID | 説明                                           |
|---------------|-------------------------------------------------------|
| PNP0C40       | Windows と互換性のあるボタン配列                       |
| PNP0C50       | HID-over-I²C 準拠しているデバイス                         |
| PNP0C60       | コンバーチブル型ノート パソコン ディスプレイ センサー デバイス              |
| PNP0C70       | ドッキング センサー デバイス                                    |
| PNP0D10       | 標準的なデバッグと XHCI 準拠の USB コント ローラー     |
| PNP0D15       | 標準デバッグなしの XHCI 準拠の USB コント ローラー  |
| PNP0D20       | 標準デバッグなしで EHCI 準拠の USB コント ローラー  |
| PNP0D25       | 標準的なデバッグと EHCI 準拠の USB コント ローラー     |
| PNP0D40       | SDA 標準に準拠した SD ホスト コント ローラー             |
| PNP0D80       | Windows と互換性のあるシステムの電源管理コント ローラー |



### <a name="subsystem-id-sub-hardware-revision-hrv-and-class-cls"></a>サブシステム ID (\_SUB)、ハードウェアのリビジョン (\_HRV)、およびクラス (\_CLS)

ACPI 5.0 の定義、 \_SUB、 \_HRV、および\_CLS オブジェクトと共に使用できる、\_より一意に特定のバージョン、統合、または、デバイスのハードウェアのリビジョンを識別する識別子を作成する HID またはデバイスの PCI 定義クラスでのメンバーシップを示します。 これらのオブジェクトは一般に省略できますが Windows で特定のデバイス クラスで必要があります。 これらのオブジェクトの詳細については、の 6.1、「デバイスの Id オブジェクト」のセクションを参照して、 [ACPI 5.0 仕様](https://uefi.org/specifications)します。

保守性の OEM システムでデバイス Id は、「4 部構成」の Id である Windows ハードウェア認定キット (HCK) 要件があります。 4 つの部分は、仕入先 ID、デバイス ID、サブシステムの製造元 (OEM) ID、およびサブシステム (OEM) デバイス id。 サブシステム ID ではそのため、(\_SUB) オブジェクトが OEM プラットフォームに必要です。

### <a name="device-specific-method-dsm"></a>デバイス固有のメソッド (\_DSM)

\_9.14.1 で DSM メソッドが定義されている"\_DSM (デバイスの特定のメソッド)"の[ACPI 5.0 仕様](https://uefi.org/specifications)します。 このメソッドは、個々 のデバイス固有のデータとデバイス ドライバーなど他のデバイスに固有のメソッドで競合することがなく呼び出すことができるコントロール関数を提供します。 \_DSM は、特定のデバイスまたはデバイス クラスの定義、UUID (GUID) が、その他の Uuid と衝突しないように保証されています。 定義されている関数のセットがある各 UUID では、を\_またはドライバーの制御関数を実行するデータを提供する DSM メソッドを実装できます。 別のデバイス固有クラス仕様で提供されるクラスに固有のデータとデータ形式も記載されて[ACPI デバイス固有のメソッド](acpi-device-specific-methods.md)します。

### <a name="address-adr-and-unique-id-uid"></a>アドレス (\_ADR) と一意の ID (\_UID)

デバイス id の 3 つの追加要件があります。

-   (たとえば、SDIO、USB HSIC)、ハードウェアの列挙可能な親バスに接続するが、プラットフォーム固有の機能やコントロール (側波帯電源または割り込みウェイク) があるデバイスの場合、 \_HID は使用されません。 代わりに、デバイス id は、(前述)、親のバス ドライバーによって作成されます。 ここでは、アドレス オブジェクト (\_ADR) デバイスを ACPI 名前空間に存在するが必要です。 このオブジェクトは、バスで列挙されるデバイスをその ACPI 説明されている機能やコントロールに関連付けるためのオペレーティング システムを使用できます。
-   プラットフォームが、特定の IP ブロックの複数のインスタンスが使用されている各ブロックがある同じデバイス識別オブジェクト、一意の識別子を持つように (\_UID) オブジェクトがブロックを区別する、オペレーティング システムを有効にするために必要です。
-   特定の名前空間スコープで 2 台のデバイスでは、同じ名前を持つことができます。

## <a name="device-configuration-objects"></a>デバイスの構成オブジェクト


名前空間で識別されるデバイスごとに、デバイスによって消費されるシステム リソース (メモリ アドレス、割り込み、) も報告する必要が現在のリソースの設定によって (\_CRS) オブジェクト。 複数の可能なリソース構成のレポート (\_PR) とデバイスのリソースの構成を変更するためのコントロール (\_SRS) はサポートされているが、省略可能。

新しい SoC プラットフォームは、GPIO、デバイスが使用できるシンプルな周辺機器バス (SPB) リソースです。 詳細については、次を参照してください。[一般的な目的 I/O (GPIO)](general-purpose-i-o--gpio-.md)と[単純な周辺機器バス (SPB)](simple-peripheral-bus--spb-.md)します。

また新しい SoC プラットフォームでは、汎用的な固定 DMA 記述子です。 FixedDMA 記述子は、多数のシステム デバイスによって、DMA コント ローラーのハードウェアの共有をサポートします。 FixedDMA 記述子には、特定のシステム デバイスに静的に割り当てられている DMA リソース (要求行とチャネル レジスタ) が一覧表示します。 詳細については、セクション、19.5.49"FixedDMA (DMA リソース記述子マクロ)"を参照してください、 [ACPI 5.0 仕様](https://uefi.org/specifications)します。

### <a name="device-status-changes"></a>デバイス状態の変更

デバイスを ACPI 列挙を無効にしたり、さまざまな理由から削除することができます。 状態 (\_STA) オペレーティング システムに伝達するには、このような状態変更を有効にするオブジェクトが提供されます。 説明については\_、STA の 6.3.7」セクションを参照してください、 [ACPI 5.0 仕様](https://uefi.org/specifications)します。 Windows を使用して\_STA を決定するかどうか、デバイス列挙、表示されるは、無効になっている、またはユーザーには表示されません。 ファームウェアでは、このコントロールは、多くのドッキングを含む、アプリケーションとホストの機能の切り替えを USB OTG に適しています。

さらに、ACPI ASL を使用して、デバイスの dock の一部として削除されるなど、プラットフォームでのイベントのドライバーを通知に通知メカニズムを提供します。 一般に、ACPI デバイスの状態が変更されたときに、ファームウェア実行する必要あります「デバイスの確認」または「チェックをバス」の通知がデバイスを再列挙を再評価するために Windows の\_の STA ACPI の通知については、5.6.6、「デバイス オブジェクトの通知」のセクションを参照して、 [ACPI 5.0 仕様](https://uefi.org/specifications)します。

## <a name="enabledisable"></a>有効化/無効化


Windows のプラグ アンド プレイの一環として、ドライバーがあることのできる動的に有効になっており、ユーザー、または (たとえば、ドライバーを更新する) のシステムを無効になっています。

SoC のデバイスでは、SoC チップが統合され、削除することはできません。 ほとんどの SoC にデバイス ドライバーは、有効化と無効にするための要件から除外できます。 除外されていないドライバー、ドライバーが正しく削除をサポートしていることを示すためのドライバー インターフェイスがあります。 詳細については、"削減 PNP 要件の SoC Drivers"をという名前のドキュメントを参照してください、 [Microsoft Connect web サイト](https://aka.ms/connect-redirect?DownloadID=47560)します。

ドライバーが所定の削除をサポートしている、デバイスのハードウェアが無効にする場合 (つまり、その割り当てられたリソースへのアクセスを停止するデバイスを構成できます)、デバイスを ACPI 名前空間ノードは、無効化を含めることができ、(\_DIS) オブジェクト。 このメソッドは、ドライバーが削除されるたびに、オペレーティング システムによって評価されます。 使用\_DIS が次の追加要件。

-   \_STA は、デバイスが無効になっているときに、「有効になっているし、そのリソースをデコード」のビットをクリアする必要があります。
-   デバイスは、セットのリソース設定を提供する必要があります (\_SRS) オブジェクトをデバイスのハードウェアを再度有効にし、上記のビットを設定\_の STA

詳細については、6.2.3 のセクションを参照してください (\_DIS)、6.2.15 (\_SRS)、および 6.3.7 (\_STA) の[ACPI 5.0 仕様](https://uefi.org/specifications)します。

## <a name="device-dependencies"></a>デバイスの依存関係


通常、特定のプラットフォーム上のデバイス間ではハードウェアの依存関係があります。 Windows では、すべてのデバイスが動的に、システム機能モ ノの変更として正しくすることを確認できるように、このようなすべての依存関係が記述されている必要があります (デバイスの電源が削除され、ドライバーを停止および起動など)。 ACPI でデバイス間の依存関係は、次の方法で説明します。

1.  **Namespace 階層**します。 (別のデバイスの名前空間内のデバイスとして表示) の子デバイスは、任意のデバイスでは、親デバイスに依存します。 たとえば、USB HSIC デバイスはポート (親) に依存してコント ローラー (親) に接続されています。 同様に、システムのメモリ管理ユニット (MMU) デバイスの名前空間内に一覧表示、GPU デバイスは MMU デバイスに依存します。
2.  **リソースの接続**します。 GPIO または SPB コント ローラーに接続されているデバイスでは、これらのコント ローラーに依存します。 この種類の依存関係がデバイスの接続リソースを含めることで説明されている\_CRS します。
3.  **依存関係の OpRegion**します。 OpRegions を使用して、I/O を実行する ASL 制御方法、依存関係は暗黙的に不明、オペレーティング システムによってのみコントロール メソッドの評価中に決定されるためです。 この問題は、GeneralPurposeIO とプラグ アンド プレイ ドライバーが、リージョンへのアクセスを提供する GenericSerialBus OpRegions に特に適用されます。 この問題を軽減するために、ACPI が OpRegion 依存関係を定義します (\_DEP) オブジェクト。 \_参照先の OpRegion の接続リソースの制御方法によって、OpRegion (HW リソース) が参照されているし、1 も上記の 2 を既に適用、デバイスの名前空間で DEP を使用してください。 詳細については、セクション 6.5.8 を参照してください。"\_DEP (処理領域の依存関係)"、の、 [ACPI 5.0 仕様](https://uefi.org/specifications)します。

デバイス ドライバーの間はソフトウェアの依存関係はできますがあります。 これらの依存関係も記載されている必要があります。 詳しくは、次のリソースをご覧ください。

-   ドライバーの読み込み順序の依存関係は、次を参照してください。[ドライバーの読み込み順序を指定する](https://docs.microsoft.com/windows-hardware/drivers/install/specifying-driver-load-order)します。
-   電源関係の依存関係を参照してください。

    -   [**IoInvalidateDeviceRelations** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicerelations)ルーチン (電源関係を確立することをトリガーする呼び出し、 **IoInvalidateDeviceRelations**ルーチン、**デバイス\_の関係\_入力**列挙型値**PowerRelations**)。
    -   [**IRP\_MN\_クエリ\_デバイス\_リレーション**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)
    -   [バス上のデバイスを列挙します。](https://docs.microsoft.com/windows-hardware/drivers/wdf/enumerating-the-devices-on-a-bus)
    -   [動的な列挙型](https://docs.microsoft.com/windows-hardware/drivers/wdf/dynamic-enumeration)
    -   [**WdfDeviceInitSetPnpPowerEventCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)メソッド








