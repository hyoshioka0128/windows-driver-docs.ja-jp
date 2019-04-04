---
title: 内蔵カメラの位置を特定する
description: このトピックでは、Windows 8.1 でのシステムで内蔵カメラのサポートについての情報を提供します。
ms.assetid: 7664F0F6-BD95-4919-82E4-F6F8080C2B5B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af9bc003e24c90fa776d8161af8879e8ca9d1fc6
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463960"
---
# <a name="identifying-the-location-of-internal-cameras-uwp-device-apps"></a>内蔵カメラ (UWP デバイス アプリ) の場所を識別します。


このトピックでは、Windows 8.1 でのシステムで内蔵カメラのサポートについての情報を提供します。 これには、UWP アプリで正しく動作するために、組み込みのカメラの物理的な場所を特定する方法について説明します。 UWP デバイス アプリを使用して、カメラが動作するように、モデル ID を設定する方法も説明します。 一般に UWP デバイス アプリの詳細について、[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)を参照してください。

## <a name="span-idprovidingphysicallocationspanspan-idprovidingphysicallocationspanspan-idprovidingphysicallocationspanproviding-physical-location"></a><span id="Providing_physical_location"></span><span id="providing_physical_location"></span><span id="PROVIDING_PHYSICAL_LOCATION"></span>物理的な場所を提供します。


機械的に固定の方向を持つ組み込みのカメラでシステムには、カメラの物理的な場所を報告する必要があります。 この物理的な場所の情報は、カメラを使用して、Windows 8.1 でのアプリが正しく機能するようなど前面または背面カメラが向いている方向を示します。

次の 2 つ[Windows ハードウェア認定要件](https://go.microsoft.com/fwlink/p/?LinkId=320504)カメラの場所を認識する Windows を使用できることが必要です。

-   **System.Client.PCContainer.PCAppearsAsSingleObject**. カメラは、コンピューター内に物理的にあるデバイス関数を含むコンピューターのデバイス コンテナーにグループ化する必要があります。 外部コンピューター コンテナーにデバイスの方向が機械的に固定されないと見なされますので、その物理的な場所に、アプリを公開する、コンピューターのデバイスのコンテナーにカメラをグループ化する必要があります。

-   **System.Client.Webcam.PhysicalLocation**します。 ファームウェアを使用して物理的な場所の情報を提供する必要があります、 \_PLD 情報、カメラの向きと場所を示すために、ACPI テーブルにします。

### <a name="span-idwhydoeswindowsneedthephysicallocationcamerasspanspan-idwhydoeswindowsneedthephysicallocationcamerasspanspan-idwhydoeswindowsneedthephysicallocationcamerasspanwhy-does-windows-need-the-physical-location-cameras"></a><span id="Why_does_Windows_need_the_physical_location_cameras_"></span><span id="why_does_windows_need_the_physical_location_cameras_"></span><span id="WHY_DOES_WINDOWS_NEED_THE_PHYSICAL_LOCATION_CAMERAS_"></span>Windows 上に物理的な場所のカメラが必要なはなぜですか。

Windows では、次の理由で内蔵カメラの物理的な場所を把握する必要があります。

-   UWP アプリでは、物理的な場所を使用して、複数のカメラが存在する場合に使用するには、どのカメラを決定します。 たとえば、チャット アプリケーションが既定のアプリの起動時に、ユーザーが直面しているフロント カメラを使用してになります。
-   UWP アプリでは、物理的な場所を使用して、ミラー化、またはビデオのプレビューを回転する方法を決定します。
-   カメラが、ユーザー、直面している場合、ユーザーがミラーに探している場合、プレビューになります。 これを行うには、アプリで反転、プレビューの左側および右側のプレビュー ビデオを反映するようにします。 ユーザーから離れるよう、カメラが直面している場合、アプリが、ビデオをミラー化する必要はありません。
-   アプリが、プレビューを回転する場合の回転角度は、カメラの位置によって異なります。

### <a name="span-idhowtogroupthecameraintothecomputersdevicecontainerspanspan-idhowtogroupthecameraintothecomputersdevicecontainerspanspan-idhowtogroupthecameraintothecomputersdevicecontainerspanhow-to-group-the-camera-into-the-computers-device-container"></a><span id="How_to_group_the_camera_into_the_computers_device_container"></span><span id="how_to_group_the_camera_into_the_computers_device_container"></span><span id="HOW_TO_GROUP_THE_CAMERA_INTO_THE_COMPUTERS_DEVICE_CONTAINER"></span>カメラをコンピューター デバイス コンテナーにグループ化する方法

認定要件に従って**System.Client.PCContainer.PCAppearsAsSingleObject**とも呼ばれますの SYSFUND 0200 PC デバイス コンテナーの下で、内部のカメラのデバイス ノードをグループ化する必要があります。 つまり、内部のカメラに表示されるされません**デバイスとプリンター**し、PC のコンテナーに統合する必要があります。

この要件を実装する方法は、内部のカメラのバスの種類によって異なります。 含めることによって、ACPI レイヤーで適切なグループ化を指定できます、デバイスは、ACPI テーブル内の物理デバイスの場所に関する情報を公開できますが場合、 \_PLD については、テーブルと」の説明に従って、ACPI テーブルで UserVisible フラグを変更します。[多機能デバイスのサポートとデバイスのコンテナー グループ分け](https://go.microsoft.com/fwlink/p/?LinkId=320505)します。 それ以外の場合、DeviceOverrides のレジストリ キーを使用してリムーバブル フラグをオーバーライドします。 詳細については、[DeviceOverrides レジストリ キー](https://go.microsoft.com/fwlink/p/?LinkId=320506)を参照してください。

### <a name="span-idhowtoprovidephysicallocationusingpldinfointheacpitablespanspan-idhowtoprovidephysicallocationusingpldinfointheacpitablespanspan-idhowtoprovidephysicallocationusingpldinfointheacpitablespanhow-to-provide-physical-location-using-pld-info-in-the-acpi-table"></a><span id="How_to_provide_physical_location_using__PLD_info_in_the_ACPI_table"></span><span id="how_to_provide_physical_location_using__pld_info_in_the_acpi_table"></span><span id="HOW_TO_PROVIDE_PHYSICAL_LOCATION_USING__PLD_INFO_IN_THE_ACPI_TABLE"></span>物理的な場所を使用して提供する方法\_ACPI テーブル PLD 情報

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

アドレスを指定する (\_ADR)、これらの手順に従います。

1.  対象の PC に Windows をインストールします。
2.  移動して**デバイス マネージャー**
3.  ターゲット、webacm を右クリックして**プロパティ**
4.  開く、**詳細**タブ**アドレス**で、**プロパティ**メニュー
5.  値、**値**ボックスは、デバイスにあるアドレス
6.  値を設定\_ADR ACPI テーブル
7.  設定、 \_ACPI 仕様と PC の設計に基づいて、PLD 値

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

## <a name="span-idprovidingmodelidspanspan-idprovidingmodelidspanspan-idprovidingmodelidspanproviding-model-id"></a><span id="Providing_Model_ID"></span><span id="providing_model_id"></span><span id="PROVIDING_MODEL_ID"></span>モデル ID を指定します。


Windows デバイスのメタデータ システムはカメラのデバイス ノードがある場合にのみ内部的に埋め込みのカメラのデバイス メタデータ パッケージのクエリを実行すること、**モデル ID**プロパティおよびデバイスのカテゴリは`Imaging.Webcam`します。 内部のカメラのメタデータ探索可能にする Windows によって、デバイス メタデータ パッケージは、デバイスと、カメラに固有の UWP デバイスのアプリに正しく関連付けられているように、OEM は、以下を行う必要があります。

-   設定、**モデル ID**を使用して、[デバイス] ノードで、`InternalDeviceModification`デバイスのレジストリ キーのフラグ

### <a name="span-idhowtosetthemodelidfortheinternalcamerasdevicenodespanspan-idhowtosetthemodelidfortheinternalcamerasdevicenodespanspan-idhowtosetthemodelidfortheinternalcamerasdevicenodespanhow-to-set-the-model-id-for-the-internal-cameras-device-node"></a><span id="How_to_set_the_Model_ID_for_the_internal_camera_s_device_node"></span><span id="how_to_set_the_model_id_for_the_internal_camera_s_device_node"></span><span id="HOW_TO_SET_THE_MODEL_ID_FOR_THE_INTERNAL_CAMERA_S_DEVICE_NODE"></span>内蔵カメラのデバイス ノードのモデル ID を設定する方法

内蔵のカメラは、OEM は、モデル ID を使用する GUID を作成し、そのレジストリ キーを作成します。 **モデル ID**プロパティは、特定のデバイスにマップするレジストリ キーから成るレジストリ ベースのルックアップ テーブル (LUT) である InternalDeviceModification メカニズムを使用して、[デバイス] ノードに追加されます。 この InternalDeviceModification テーブルは、次のレジストリ キーの下で管理されます。

-   `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\InternalDeviceModification`

InternalDeviceModification のレジストリ キーを作成するサブキー、エントリは、ModelID の OEM が指定した GUID です。 このキーの存在は、デバイスのハードウェア ID に基づいて、カメラのデバイス ノードで示される場所の情報をモデル ID を追加、 \_ACPI テーブル PLD 値。

![レジストリ キーと値の internaldevicemodification](images/372985-camera-internal-registry-layout.png)

### <a name="span-idinternaldevicemodificationregistrykeyspanspan-idinternaldevicemodificationregistrykeyspanspan-idinternaldevicemodificationregistrykeyspaninternaldevicemodification-registry-key"></a><span id="InternalDeviceModification_registry_key"></span><span id="internaldevicemodification_registry_key"></span><span id="INTERNALDEVICEMODIFICATION_REGISTRY_KEY"></span>InternalDeviceModification レジストリ キー

InternalDeviceModification のレジストリ キーでは、その 1 つ以上のカメラ、ModelID を使用することを示します。

|                     |                                                                                  |
|---------------------|----------------------------------------------------------------------------------|
| レジストリ キーの名前   | `InternalDeviceModification`                                                     |
| 必須/省略可能   | 必須                                                                         |
| パス                | `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control`                            |
| 形式の要件 | なし                                                                             |
| 有効なサブキー       | モデル ID のレジストリ キー (次のサブキーの形式の要件と examles 参照) |

 

### <a name="span-idmodelidregistrykeyspanspan-idmodelidregistrykeyspanspan-idmodelidregistrykeyspanmodel-id-registry-key"></a><span id="Model_ID_registry_key"></span><span id="model_id_registry_key"></span><span id="MODEL_ID_REGISTRY_KEY"></span>モデル ID のレジストリ キー

|                     |                                                                                            |
|---------------------|--------------------------------------------------------------------------------------------|
| レジストリ キーの名前   | モデル ID (ID 値の正確なモデルでは、キー名)                                            |
| 必須/省略可能   | 必須                                                                                   |
| 形式の要件 | キー名は、OEM によって作成された GUID です。 開始と終了の角かっこの両方が必要です。 |
| 有効な値        | ハードウェア ID のレジストリ値または `PLD_Panel`                                                 |
| 使用例            | `{43922620-DAD9-4C05-BE3F-F65B089D84D8}`                                                   |

 

### <a name="span-idhardwareidregistryvaluespanspan-idhardwareidregistryvaluespanspan-idhardwareidregistryvaluespanhardware-id-registry-value"></a><span id="Hardware_ID_registry_value"></span><span id="hardware_id_registry_value"></span><span id="HARDWARE_ID_REGISTRY_VALUE"></span>ハードウェア ID のレジストリ値

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">レジストリ値の名前</td>
<td align="left">HardwareIDs</td>
</tr>
<tr class="even">
<td align="left">必須/省略可能</td>
<td align="left">必須</td>
</tr>
<tr class="odd">
<td align="left">型</td>
<td align="left">複数の文字列</td>
</tr>
<tr class="even">
<td align="left">形式の要件</td>
<td align="left">ハードウェア ID のバスのプレフィックスを含める必要があります。 すべて"&amp;quot;文字は、「#」で置き換える必要があります。</td>
</tr>
<tr class="odd">
<td align="left">使用例</td>
<td align="left"><p><code>USB#VID_1234&amp;PID_ABCD&amp;REV_0001</code></p>
<p><code>PCI#VEN_ABCD&amp;DEV_1234&amp;SUBSYS_000</code></p></td>
</tr>
<tr class="even">
<td align="left">Comment</td>
<td align="left">複数のハードウェア ID の値を指定することができます。 システムがハードウェア ID に基づいてデバイス ノードのモデル ID を設定するハードウェア Id のいずれかが発生した場合、一覧で複数回、</td>
</tr>
</tbody>
</table>

 

### <a name="span-idpldpanelregistryvaluespanspan-idpldpanelregistryvaluespanspan-idpldpanelregistryvaluespanpldpanel-registry-value"></a><span id="PLD_Panel_registry_value"></span><span id="pld_panel_registry_value"></span><span id="PLD_PANEL_REGISTRY_VALUE"></span>PLD\_レジストリ値パネル

|                     |                                                                                                  |
|---------------------|--------------------------------------------------------------------------------------------------|
| レジストリ値の名前 | `PLD_Panel`                                                                                      |
| 必須/省略可能   | 省略可能                                                                                         |
| 型                | DWORD                                                                                            |
| 形式の要件 | HardwareID のバスのプレフィックスを含める必要があります。 すべて"\\"文字を置換する必要がある、"\#"。 |
| 使用例            | 4,5                                                                                              |

 

### <a name="span-idpldpaneldetailsspanspan-idpldpaneldetailsspanspan-idpldpaneldetailsspanpldpanel-details"></a><span id="PLD_Panel_Details"></span><span id="pld_panel_details"></span><span id="PLD_PANEL_DETAILS"></span>PLD\_詳細パネル

PLD\_ACPI テーブルで指定されたパネル値により、システムが 2 つの同一のカメラ デバイスありどちらも同一のハードウェア Id 場合に、互いに識別するカメラ。 別のモデル Id、PLD とハードウェア Id の組み合わせを作成する\_パネルの値が使用されます。

**注**  、PLD\_パネルの設定のレジストリ キーには省略可能です。 Windows では、ACPI テーブルの設定によって、カメラの物理的な場所を決定します。

 

PLD\_としてパネル レジストリ値が定義されている\_ACPI 仕様で PLD (物理デバイスの場所)。 この値は、エンクロージャ内のカメラの物理的な場所を示すは、次のいずれかである必要があります。

| 値 | 説明                                                         |
|-------|---------------------------------------------------------------------|
| 0     | Top                                                                 |
| 1     | Bottom                                                              |
| 2     | Left                                                                |
| 3     | 右                                                               |
| 4     | 前面                                                               |
| 5     | Back                                                                |
| 6     | 不明な (垂直方向の位置と水平方向の位置が無視されます) |

 

### <a name="span-idinternaldevicemodificationregistrykeyexamplesspanspan-idinternaldevicemodificationregistrykeyexamplesspanspan-idinternaldevicemodificationregistrykeyexamplesspaninternaldevicemodification-registry-key-examples"></a><span id="InternalDeviceModification_registry_key_examples"></span><span id="internaldevicemodification_registry_key_examples"></span><span id="INTERNALDEVICEMODIFICATION_REGISTRY_KEY_EXAMPLES"></span>InternalDeviceModification レジストリ キーのサンプル

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

### <a name="span-idmetadatastructurespanspan-idmetadatastructurespanspan-idmetadatastructurespanmetadata-structure"></a><span id="Metadata_structure"></span><span id="metadata_structure"></span><span id="METADATA_STRUCTURE"></span>メタデータ構造体

内部のカメラのデバイス メタデータ パッケージには、その他のデバイスのデバイス メタデータ パッケージと同じ構造があります。 MetadataKey **packageinfo.xml**デバイス メタデータ パッケージは InternalDeviceModification のレジストリ キーを使用して定義されているモデルの ID。 Windows メタデータ システムは、モデルの ID に基づくデバイス メタデータ パッケージをダウンロードします。 内部のカメラのハードウェア ID は使用されません。

UWP デバイス アプリのデバイス メタデータを作成する方法の詳細については、[構築 UWP デバイス アプリ](the-workflow.md)を参照してください。

### <a name="span-idpre-installationspanspan-idpre-installationspanspan-idpre-installationspanpre-installation"></a><span id="Pre-installation"></span><span id="pre-installation"></span><span id="PRE-INSTALLATION"></span>インストール前

Microsoft Store のデバイス アプリとデバイス メタデータ パッケージの両方は、OEM プレインストール キット (OPK) を使用してデバイス上にプレインストールされていることができます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[内部デバイス用の UWP デバイス アプリ](uwp-device-apps-for-specialized-devices.md)

 

 






