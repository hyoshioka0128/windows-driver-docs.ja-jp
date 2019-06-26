---
title: カメラの向きのドライバー サポート
description: デバイスのカメラの向きを明示的に指定する方法について説明します。
ms.date: 08/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: 63a4a75c684aa7bba39853636ce171edc432ac63
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386692"
---
# <a name="driver-support-for-camera-orientation"></a>カメラの向きのドライバー サポート



> [!IMPORTANT]
> このトピックの後半で説明されている自動修正のメソッドは、*推奨*カメラ センサーの非参照向きマウント ソリューション。 これは、既にフィードがチェックされ、また、ローテーションの情報の修正に不明なカメラを使用するように記述するアプリケーションの大部分からアプリの互換性を確保します。 次の自動修正セクションの情報を慎重に確認してください。

以降、Window 10 バージョン 1607 をでカメラのすべてのドライバーはに従って、カメラがマウントされている場合に関係なく、カメラの向きを明示的に指定する必要な[ハードウェアの最小要件](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview)します。

具体的には、カメラのドライバーが新しいに設定する必要があります**回転**フィールドに、ACPI \_PLD 構造体がキャプチャ デバイスのインターフェイスに関連付けられています。

```cpp
typedef struct _ACPI_PLD_V2_BUFFER {

    UINT32 Revision:7;
    UINT32 IgnoreColor:1;
    UINT32 Color:24;
    // ...
    UINT32 Panel:3; // Already supported by camera.
    // ...
    UINT32 CardCageNumber:8;
    UINT32 Reference:1;
    UINT32 Rotation:4;  // 0 – Rotate by 0° clockwise
                        // 1 – Rotate by 45° clockwise (N/A to camera)
                        // 2 – Rotate by 90° clockwise
                        // 3 – Rotate by 135° clockwise (N/A to camera)
                        // 4 – Rotate by 180° clockwise
                        // 5 – Rotate by 225° clockwise (N/A to camera)
                        // 6 – Rotate by 270° clockwise
     UINT32 Order:5;
     UINT32 Reserved:4;

     //
     // _PLD v2 definition fields.
     //

     USHORT VerticalOffset;
     USHORT HorizontalOffset;

 } ACPI_PLD_V2_BUFFER, *PACPI_PLD_V_BUFFER;
 ```

カメラ、**回転**フィールド、ACPI に\_PLD 構造数を指定する、表示中には、キャプチャされたフレームを画面を基準と回転するよう度 ('0 'が 0 °、90 °、180 ° の' 4' を '2' と' 6' 270 ° の) のネイティブの方向。

値に基づいて、**回転**フィールドに、アプリケーションを実行できます追加回転は、必要に応じて、正常にキャプチャされたフレームをレンダリングするためにします。

## <a name="design-overview"></a>設計の概要


共有同じハウジングのカメラとが表示されますが、これらのデバイスまたは*エンクロージャ*/*大文字小文字の区別*(スマート フォン、タブレット、ノートブック、および Pc をすべて 1 つ) がこれらの周辺機器があるとすることができます各 (通常は 0、90、180、または実際には時計回りに 270 度に制限されます) それぞれその平面上の固定まだ任意度回転されているうちに別の場所 (フロント、上/下、または、エンクロージャのサーフェイスを左/右) でマウントされます。 カメラとしてこのカテゴリに従来のデスクトップ Pc も分類されないことと表示は、通常、外付け周辺機器として接続し、実行時に 3 次元空間で物理的に操作できることができますに注意してください。

その結果、アプリケーションには、キャプチャされたフレームをレンダリング サーフェイスの向きが正しい転置できるように 2 つの周辺機器の空間関係を記述するためのメカニズムが必要があります。

問題を解決する 1 つの方法は、ACPI を使用する\_PLD が構造体がの概念は既に*画面*と*の回転角度*定義します。 参照してください、 [ACPI 仕様](https://uefi.org/specifications)と[ACPI サポート ドキュメント](https://uefi.org/acpi)の完全な仕様。 たとえば、 \_PLD 構造が既に*パネル*周辺機器が存在する画面を指定するフィールド。

![ACPI PLD パネル フィールド](images/acpi-pld-panel-field.png)

*ACPI の定義\_PLD パネル フィールド (Rev. 5.0 a)*

次の 2 つの図は、各パネルの定義を視覚的に説明します。

![パネルの定義 - デスクトップ](images/panel-definitions-desktop.png)

*デスクトップ Pc、およびほとんどのデバイスのパネルの定義*

![パネルの定義 - たたみ込み可能なデバイス](images/panel-definitions-foldable-devices.png)

*たたみ込み可能なデバイスのパネルの定義*

ACPI の概念*パネル*は、Windows が既に採用している場所。

-   カメラ デバイスのインターフェイスに関連付けられている、 \_PLD キャプチャ デバイスは静的に固定した場所にマウントされている場合、それに応じて設定されているパネル フィールド構造体。

-   アプリケーションが呼び出すことによってキャプチャ デバイスが存在するパネルを取得できます、 [Windows.Devices.Enumeration.DeviceInformation.EnclosureLocation.Panel](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.EnclosureLocation#Windows_Devices_Enumeration_EnclosureLocation_Panel)プロパティ。

ACPI \_PLD 構造があります、**回転**次のように定義されているフィールド。

![ACPI PLD 回転フィールド](images/acpi-pld-rotation-field.png)

*ACPI の定義\_PLD 回転フィールド (Rev 5.0 a)*

現状有姿の上の定義を使用せずにさらに修正してみましょうあいまいさを避けるために。

- カメラ、**回転**フィールド、ACPI に\_PLD 構造数を指定する、表示中には、キャプチャされたフレームを画面を基準と回転するよう度 ('0 'が 0 °、90 °、180 ° の' 4' を '2' と' 6' 270 ° の) のネイティブの方向。

## <a name="landscape-primary-vs-portrait-primary"></a>プライマリとランドス ケープ縦のプライマリ

ランドス ケープのプライマリまたは縦プライマリとして定義できますデバイス フォーム ファクター、によって、このから返される値として定義されて[Windows.Graphics.Display.DisplayInformation.NativeOrientation](https://docs.microsoft.com/uwp/api/Windows.Graphics.Display.DisplayInformation#Windows_Graphics_Display_DisplayInformation_NativeOrientation)プロパティ。

デバイスとは横または縦プライマリの ACPI 定義かどうかに関係なく*原点*は常に、パネルの左下隅に、ユーザーは、パネルに接続します。 カメラのセンサーの推奨されるマウント方向は、センサーのスキャン ラインが左から右下隅に、ACPI パネルの左下隅 (origin) から水平方向に右になるようです。

これは、センサーの参照の方向です。

![プライマリのランドス ケープ - センサー スキャン方向](images/landscape-primary-sensor-scan-direction.png)

*プライマリのランドス ケープ:センサーのスキャン方向*

同様に、縦プライマリの参照の向き、センサーが下に図示として。

![縦のプライマリのセンサーのスキャン方向](images/portrait-primary-sensor-scan-direction.png)

*縦 Primary:センサーのスキャン方向*

これにより、ジャイロ/加速度計センサーでは、デバイスの相対的な方向の通知を生成するときジャイロ/加速度計の参照ポイントは、センサーの参照の向きで一貫性のあります。つまり、アプリがデバイスの相対的な方向を取得だけですとその情報のみに基づいてメディアのフレームを調整することができます。

## <a name="non-reference-orientation-mounting"></a>非参照向きのマウント


ハードウェア/フォーム ファクターの制約がある多くの場合、センサーは参照方向からのオフセットにマウントする必要があります。 これが完了したら、OEM/IHV は次の 2 つのソリューションのいずれかを実装する必要があります。

1.  **推奨**:自動では、印刷の向きを修正します。 センサー ドライバーとカメラのドライバーは、結果として得られるフレームを「修正」カメラ ドライバー スタックを現在のセンサーの方向を示す 2 つのドライバーの間のカスタム プロトコルを作成する必要があります。

2.  内のオフセットを示す、 \_PLD**回転**フィールド。

### <a name="auto-correct"></a>自動修正

これは、*推奨*参照方向マウント カメラ センサーのソリューションです。 これは、既にフィードがチェックされ、また、ローテーションの情報の修正に不明なカメラを使用するように記述するアプリケーションの大部分からアプリの互換性を確保します。

これには、DirectShow アプリケーションおよび MF/MediaCapture ベースのアプリケーションのほとんどが含まれます。

> [!NOTE]
> Oem および Ihv を使用して、センサーの実際の向きのアドバタイズでする必要がありますしない自動修正を使用する場合、 \_PLD**回転**フィールド。 ここで、**回転**フィールドは、修正した後、印刷の向きを示す必要があります。0 度です。

### <a name="pld-rotation"></a>\_PLD 回転

ハードウェアの制約がシステムからキャプチャされたフレームを自動修正を回転に対応するアプリで補うことができますので、参照方向からのオフセットを示すために推奨されるソリューションを制限するかどうか。

このソリューションは理想的なかので、前述のように、多くの既存アプリケーションはない処理 (いることも) 参照方向**回転**情報。 これにより、アプリケーションがどこでキャプチャして、正しくない向きでビデオ フレームのレンダリングを終了重要なアプリケーションの互換性の問題が発生します。

次の図は、の値を示して、 \_PLD**回転**ハードウェア構成ごとにフィールド。

**回転:0 度時計回り (参照方向)**

![-0 度時計回りの回転の参照の方向](images/rotation-0-degree-reference-orientation.png)

上の図には。

-   左側の図は、キャプチャするシーンを示しています。

-   中央の画像は表示領域の物理順序が左から右方向の移動、左下隅から開始 CMOS センサーでシーンを表示する方法を示しています。 ハードウェアのレベルでは、この例では、CMOS センサーは、いない水平、垂直方向にシーンを反転します。

-   右側の画像では、カメラのドライバーの出力を表します。 この例では、メディアのバッファーの内容を表示できます直接表示がさらに回転せずネイティブの方向。 その結果、ACPI \_PLD**回転**フィールドが 0 の値を持ちます。



**回転:時計回りに 90 度**

![時計回りに 90 度の回転](images/rotation-90-degrees-clockwise.png)

この場合、メディアのバッファーの内容は、元のシーンと比較して時計回りに 90 度回転されます。 その結果、ACPI \_PLD**回転**フィールドには 2 の値。

アプリケーションの読み取り、 \_PLD**回転**情報は、反時計回りに 90 度、結果のイメージを回転させること、イメージを修正は反時計回りにします。



**時計回りに 180 度の回転**

![時計回りに 180 度の回転](images/rotation-180-degrees-clockwise.png)

この場合、メディアのバッファーの内容は、元のシーンと比較して時計回りに 180 度回転されます。 その結果、ACPI \_PLD**回転**フィールドには 4 の値。

アプリケーションの読み取り、 \_PLD**回転**情報は反時計回り結果のイメージを 180 度回転して、イメージを修正します。



**回転:時計回りに 270 度**

![時計回りに 270 度の回転](images/rotation-270-degrees-clockwise.png)

この場合、メディアのバッファーの内容は、元のシーンと比較して時計回りに 270 度回転されます。 その結果、ACPI \_PLD**回転**フィールドには 6 の値。

アプリケーションの読み取り、 \_PLD**回転**情報は、反時計回りに 90 °、結果のイメージを回転させること、イメージが修正されると (270 度と同じカウンター右回りに)。


