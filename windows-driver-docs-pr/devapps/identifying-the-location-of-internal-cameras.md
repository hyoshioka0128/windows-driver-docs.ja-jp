---
title: 内蔵カメラの位置を特定する
description: このトピックでは、Windows 8.1 でのシステムで内蔵カメラのサポートについての情報を提供します。
ms.assetid: 7664F0F6-BD95-4919-82E4-F6F8080C2B5B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8df64139670eb4652e308ee56ad17cba9338061e
ms.sourcegitcommit: 707739250ebdcd74a26d85d8b4217fa81c9c9e95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68181285"
---
# <a name="identifying-the-location-of-internal-cameras-uwp-device-apps"></a>内蔵カメラ (UWP デバイス アプリ) の場所を識別します。

このトピックでは、Windows 8.1 でのシステムで内蔵カメラのサポートについての情報を提供します。 これには、UWP アプリで正しく動作するために、組み込みのカメラの物理的な場所を特定する方法について説明します。 UWP デバイス アプリを使用して、カメラが動作するように、モデル ID を設定する方法も説明します。 一般に UWP デバイス アプリの詳細について、次を参照してください。[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)します。

## <a name="providing-physical-location"></a>物理的な場所を提供します。

機械的に固定の方向を持つ組み込みのカメラでシステムには、カメラの物理的な場所を報告する必要があります。 この物理的な場所の情報は、カメラを使用して、Windows 8.1 でのアプリが正しく機能するようなど前面または背面カメラが向いている方向を示します。

次の 2 つ[Windows ハードウェア認定要件](https://go.microsoft.com/fwlink/p/?LinkId=320504)カメラの場所を認識する Windows を使用できることが必要です。

- **System.Client.PCContainer.PCAppearsAsSingleObject**します。 カメラは、コンピューター内に物理的にあるデバイス関数を含むコンピューターのデバイス コンテナーにグループ化する必要があります。 外部コンピューター コンテナーにデバイスの方向が機械的に固定されないと見なされますので、その物理的な場所に、アプリを公開する、コンピューターのデバイスのコンテナーにカメラをグループ化する必要があります。

- **System.Client.Webcam.PhysicalLocation**します。 ファームウェアを使用して物理的な場所の情報を提供する必要があります、 \_PLD 情報、カメラの向きと場所を示すために、ACPI テーブルにします。

### <a name="why-windows-requires-the-physical-location-cameras"></a>なぜ Windows が物理的な場所のカメラが必要です。

Windows では、次の理由で内蔵カメラの物理的な場所を把握する必要があります。

- UWP アプリでは、物理的な場所を使用して、複数のカメラが存在する場合に使用するには、どのカメラを決定します。 たとえば、チャット アプリケーションが既定のアプリの起動時に、ユーザーが直面しているフロント カメラを使用してになります。
- UWP アプリでは、物理的な場所を使用して、ミラー化、またはビデオのプレビューを回転する方法を決定します。
- カメラが、ユーザー、直面している場合、ユーザーがミラーに探している場合、プレビューになります。 これを行うには、アプリで反転、プレビューの左側および右側のプレビュー ビデオを反映するようにします。 ユーザーから離れるよう、カメラが直面している場合、アプリが、ビデオをミラー化する必要はありません。
- アプリが、プレビューを回転する場合の回転角度は、カメラの位置によって異なります。

### <a name="how-to-group-the-camera-into-the-computers-device-container"></a>カメラをコンピューター デバイス コンテナーにグループ化する方法

認定要件に従って**System.Client.PCContainer.PCAppearsAsSingleObject**とも呼ばれますの SYSFUND 0200 PC デバイス コンテナーの下で、内部のカメラのデバイス ノードをグループ化する必要があります。 つまり、内部のカメラに表示されるされません**デバイスとプリンター**し、PC のコンテナーに統合する必要があります。

この要件を実装する方法は、内部のカメラのバスの種類によって異なります。 含めることによって、ACPI レイヤーで適切なグループ化を指定できます、デバイスは、ACPI テーブル内の物理デバイスの場所に関する情報を公開できますが場合、 \_PLD については、テーブルと」の説明に従って、ACPI テーブルで UserVisible フラグを変更します。[多機能デバイスのサポートとデバイスのコンテナー グループ分け](https://go.microsoft.com/fwlink/p/?LinkId=320505)します。 それ以外の場合、DeviceOverrides のレジストリ キーを使用してリムーバブル フラグをオーバーライドします。 詳細については、次を参照してください。 [DeviceOverrides レジストリ キー](https://go.microsoft.com/fwlink/p/?LinkId=320506)します。

### <a name="how-to-provide-physical-location-using-pld-info-in-the-acpi-table"></a>物理的な場所を使用して提供する方法\_ACPI テーブル PLD 情報

認定要件に従って**System.Client.Webcam.PhysicalLocation**、 \_ACPI (Advanced Configuration and Power Interface カメラの位置を示す PLD 値を指定する必要があります) テーブル。 これは、システムのシャーシに組み込まれているし、方向が修正機械的カメラ デバイスに適用されます。 ファームウェアを提供する必要があります、 \_PLD メソッド パネル フィールドを設定し、(ビット\[69:67\]) カメラがマウントされているパネルの適切な値にします。 たとえば、前面カメラ (webcam)、ユーザーに直面して、バックエンドでは、カメラがエンドユーザー (静止画またはビデオ カメラ) の反対側に面していることを示しますを示します。

| 値のビットの\[69:67\] | Panel   |
|-------------------------|---------|
| 0                       | Top     |
| 1                       | Bottom  |
| 2                       | Left    |
| 3                       | 右   |
| 4                       | 前面   |
| 5                       | Back    |
| 6                       | Unknown |

(垂直オフセット)、143:128 をさらに、ビットし、ビット 159:144 が (水平方向オフセット) が表示に関して、カメラの相対的な位置を指定する必要があります。 このオリジンによる表示コンポーネントでネイティブのピクセルのアドレス指定に対する相対パスですし、横または縦の現在の画面の向きに一致する必要があります。 原点は、正の水平スクロール バーと垂直方向のオフセット値が右側にし、それぞれ、ディスプレイの左下隅です。

USB で接続された内部のカメラの USB ポート デバイス ノードの下の ACPI テーブルの USB デバイスのデバイス ノードが作成されます。

アドレスを指定する (\_ADR)。

1. 対象の PC に Windows をインストールします。
2. 移動して**デバイス マネージャー**
3. ターゲット、webacm を右クリックして**プロパティ**
4. 開く、**詳細**タブ**アドレス**で、**プロパティ**メニュー
5. 値、**値**ボックスは、デバイスにあるアドレス
6. 値を設定\_ADR ACPI テーブル
7. 設定、 \_ACPI 仕様と PC の設計に基づいて、PLD 値

この例は、USB で接続されたカメラの ACPI テーブルです。 この例で、値は 0x1 です。 9 番目のバイトには、地域のパネルのコードが含まれています (ビット\[69:67\])。 デバイスが複合 USB デバイスの場合は、PLD がビデオの関数である必要がありますに注意してください。 つまり、Device() の追加のエントリが必要になります。

```Text
Device(PRTD)
{
     Name(_ADR, 0x6)
     Name(_UPC, Package(0x4)
     {
            ....
     }
     Name(_PLD, Buffer(0x10)
     {
            ....
     }
     Device(WCAM)
     {
           Name(_ADR, 0x6)
           Name(_PLD, Buffer(0x10) {
           0x81, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
           0x20, 0x1C, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00})
     }
}
```

詳細については、ACPI 仕様を参照してください\_PLD します。

ノードのダウン ストリーム USBCCGP の場合、カメラ関数の最初のインターフェイスの数にポート番号を追加することで、アドレスの値が計算されます。 USBCCGP がデバイスに読み込まれていない場合、アドレスは、ポート番号だけです。 Windows をインストールしなくてもアドレス数を予測する必要がある場合は、それを計算する次の数式を使用してください。 ターゲット デバイスが (複合スタイルの USB デバイスを使用して) なしの 1 つの関数のデバイスの場合は、ポート番号のみを使用して、アドレスの値が計算されます。

## <a name="providing-model-id"></a>モデル ID を指定します。

Windows デバイスのメタデータ システムはカメラのデバイス ノードがある場合にのみ内部的に埋め込みのカメラのデバイス メタデータ パッケージのクエリを実行すること、**モデル ID**プロパティおよびデバイスのカテゴリは`Imaging.Webcam`します。 内部のカメラのメタデータ探索可能にする Windows によって、デバイス メタデータ パッケージは、デバイスと、カメラに固有の UWP デバイスのアプリに正しく関連付けられているように、OEM は、以下を行う必要があります。

- 設定、**モデル ID**を使用して、[デバイス] ノードで、`InternalDeviceModification`デバイスのレジストリ キーのフラグ

### <a name="how-to-set-the-model-id-for-the-internal-cameras-device-node"></a>内蔵カメラのデバイス ノードのモデル ID を設定する方法

内蔵のカメラは、OEM は、モデル ID を使用する GUID を作成し、そのレジストリ キーを作成します。 **モデル ID**プロパティは、特定のデバイスにマップするレジストリ キーから成るレジストリ ベースのルックアップ テーブル (LUT) である InternalDeviceModification メカニズムを使用して、[デバイス] ノードに追加されます。 この InternalDeviceModification テーブルは、次のレジストリ キーの下で管理されます。

- `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\InternalDeviceModification`

InternalDeviceModification のレジストリ キーを作成するサブキー、エントリは、ModelID の OEM が指定した GUID です。 このキーの存在は、デバイスのハードウェア ID に基づいて、カメラのデバイス ノードで示される場所の情報をモデル ID を追加、 \_ACPI テーブル PLD 値。

![レジストリ キーと値の internaldevicemodification](images/372985-camera-internal-registry-layout.png)

### <a name="internaldevicemodification-registry-key"></a>InternalDeviceModification レジストリ キー

InternalDeviceModification のレジストリ キーでは、その 1 つ以上のカメラ、ModelID を使用することを示します。

|レジストリ キーの名前|`InternalDeviceModification`|
|----|----|
|必須/省略可能| 必須|
|パス|`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control`|
|形式の要件|なし|
|有効なサブキー|モデル ID のレジストリ キー (次のサブキーの形式の要件と例を参照してください)|

### <a name="model-id-registry-key"></a>モデル ID のレジストリ キー

| レジストリ キーの名前   | モデル ID (ID 値の正確なモデルでは、キー名)|
|----|----|
|必須/省略可能|必須|
|形式の要件|キー名は、OEM によって作成された GUID です。 開始と終了の角かっこの両方が必要です。 |
|有効な値|ハードウェア ID のレジストリ値または `PLD_Panel`|
| 使用例|`{43922620-DAD9-4C05-BE3F-F65B089D84D8}`|

### <a name="hardware-id-registry-value"></a>ハードウェア ID のレジストリ値

|レジストリ値の名前|HardwareIDs|
|----|----|
|必須/省略可能|必須|
|型|複数の文字列|
|形式の要件|ハードウェア ID のバスのプレフィックスを含める必要があります。 すべて""を「#」文字を置き換える必要があります。|
|使用例|`USB#VID_1234&PID_ABCD&REV_0001` <br/>`PCI#VEN_ABCD&DEV_1234&SUBSYS_000`|
|Comment|複数のハードウェア ID の値を指定することができます。 システムがハードウェア ID に基づいてデバイス ノードのモデル ID を設定するハードウェア Id のいずれかが発生した場合、一覧で複数回、|

### <a name="pldpanel-registry-value"></a>PLD\_レジストリ値パネル

| レジストリ値の名前 | `PLD_Panel`|
|----|----|
| 必須/省略可能   | 省略可能|
| 型| DWORD|
| 形式の要件 | HardwareID のバスのプレフィックスを含める必要があります。 すべて"\\"文字を置換する必要がある、"\#"。 |
| 使用例            | 4, 5|

### <a name="pldpanel-details"></a>PLD\_詳細パネル

PLD\_ACPI テーブルで指定されたパネル値により、システムが 2 つの同一のカメラ デバイスありどちらも同一のハードウェア Id 場合に、互いに識別するカメラ。 別のモデル Id、PLD とハードウェア Id の組み合わせを作成する\_パネルの値が使用されます。

**注**  、PLD\_パネルの設定のレジストリ キーには省略可能です。 Windows では、ACPI テーブルの設定によって、カメラの物理的な場所を決定します。

PLD\_としてパネル レジストリ値が定義されている\_ACPI 仕様で PLD (物理デバイスの場所)。 この値は、エンクロージャ内のカメラの物理的な場所を示すは、次のいずれかである必要があります。

| 値 | 説明|
|-------|----------|
| 0     | Top|
| 1     | Bottom|
| 2     | Left|
| 3     | 右|
| 4     | 前面|
| 5     | Back |
| 6     | 不明な (垂直方向の位置と水平方向の位置が無視されます) |

### <a name="internaldevicemodification-registry-key-examples"></a>InternalDeviceModification レジストリ キーのサンプル

次の例では、InternalDeviceModification レジストリ キーの形式を示します。

```Text
{00001111-2222-3333-4444-555566667777}
      HardwareIDs (Multi sz) =
      “USB#VID_1234&PID_ABCD&REV_0001”,“USB#VID_1234&PID_ABCD"
      PLD_Panel (DWORD) = 4
{88889999-aaaa-bbbb-cccc-ddddeeeeffff}
      HardwareIDs (multi sz) = “USB#VID_5678&PID_WXYZ&REV_0001”
      PLD_Panel (DWORD) = 5
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\InternalDeviceModification]

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\InternalDeviceModification\{BBBF38D6-9866-493D-B86F-986E339E096D}]
"PLD_Panel"=dword:00000004
"HardwareIDs"=hex(7):55,00,53,00,42,00,23,00,56,00,49,00,44,00,5f,00,30,00,34,\
  00,35,00,45,00,26,00,50,00,49,00,44,00,5f,00,30,00,30,00,31,00,30,00,23,00,\
  52,00,45,00,56,00,5f,00,30,00,30,00,30,00,31,00,00,00,55,00,53,00,42,00,23,\
  00,56,00,49,00,44,00,5f,00,30,00,34,00,35,00,45,00,26,00,50,00,49,00,44,00,\
  5f,00,30,00,30,00,31,00,30,00,00,00,00,00
```

### <a name="metadata-structure"></a>メタデータ構造体

内部のカメラのデバイス メタデータ パッケージには、その他のデバイスのデバイス メタデータ パッケージと同じ構造があります。 MetadataKey **packageinfo.xml**デバイス メタデータ パッケージは InternalDeviceModification のレジストリ キーを使用して定義されているモデルの ID。 Windows メタデータ システムは、モデルの ID に基づくデバイス メタデータ パッケージをダウンロードします。 内部のカメラのハードウェア ID は使用されません。

UWP デバイス アプリのデバイス メタデータを作成する方法の詳細については、次を参照してください。[構築 UWP デバイス アプリ](the-workflow.md)します。

### <a name="pre-installation"></a>インストール前

Microsoft Store のデバイス アプリとデバイス メタデータ パッケージの両方は、OEM プレインストール キット (OPK) を使用してデバイス上にプレインストールされていることができます。

## <a name="related-topics"></a>関連トピック

[内部デバイス用の UWP デバイス アプリ](uwp-device-apps-for-specialized-devices.md)
