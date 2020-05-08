---
title: マイク配列ジオメトリのプロパティ
description: マイク配列ジオメトリのプロパティ
ms.assetid: 7f280677-f86d-4687-b992-e2580046bd57
keywords:
- mic 配列 WDK オーディオ
- ジオメトリ記述子 WDK オーディオ
- マイクアレイ WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3cd9c8d6a805d2c853c2d13ebf4a209d1507801
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925545"
---
# <a name="microphone-array-geometry-property"></a>マイク配列ジオメトリのプロパティ


Windows Vista 以降では、マイク配列のサポートが提供されています。 ほとんどの場合、ラップトップまたはモニターに埋め込まれている1つのマイクは、サウンドを十分にキャプチャしません。 マイクの配列は、サウンドソースを分離し、アンビエントノイズとリバーブを拒否するためにパフォーマンスを向上させます。 [**Ksk\_プロパティの AUDIO\_MIC\_配列\_ジオメトリ**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-mic-array-geometry)プロパティは、マイク配列のジオメトリを指定します。 プロパティ値[**Ksk audio\_\_MIC 配列\_GEOMETRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)は、配列の型 (線形、平面など)、配列内のマイクの数、およびその他の機能について説明します。

このトピックでは、Windows Vista に付属しているマイクアレイサポートを外部 USB マイクアレイで使用する方法について説明します。 外部 USB マイク配列は、 **GET\_MEM**要求に応答して、配列のジオメトリおよびその他の機能を記述するために必要なパラメーターを提供する必要があります。

USB マイク配列では、標準形式を使用してジオメトリ情報を指定します。 Windows Vista USB オーディオクラスドライバーは、ジオメトリ情報を読み取るときに同じ形式を使用する必要があります。 標準形式の詳細については、「[マイク配列のジオメトリ記述子の形式](microphone-array-geometry-descriptor-format.md)」を参照してください。

アプリケーションでは、 [Ipart:: GetSubType](https://docs.microsoft.com/windows/win32/api/devicetopology/nf-devicetopology-ipart-getsubtype)を呼び出してジャックに関する情報を取得し、ジャックに接続されているデバイスがマイク配列であるかどうかを判断できます。 **Ipart:: GetSubType**は、入力ジャックの種類を表すピンカテゴリの GUID を返します。 接続されているデバイスがマイク配列の場合、返される GUID は KSNODETYPE\_マイク\_配列と同じになります。 また、マイク配列を間違ったジャックに接続しているかどうかを判断するのにも役立ちます。 後者のシナリオでは、返されるピンカテゴリの GUID は、別のデバイス用か、マイクジャックに接続されているデバイスがないことを示します。 Pin カテゴリの Guid の詳細については、「[ピンカテゴリのプロパティ](pin-category-property.md)」を参照してください。

アプリケーションが、正しい入力ジャックに接続されているマイク配列を検出したら、次の手順では配列のジオメトリを決定します。 基本ジオメトリには、*線形*、*平面*、 *3 次元 (3-d)* の3つがあります。 また、各マイクの周波数範囲や x-y 座標などの詳細も表示されます。

次のコード例は、外部 USB\_マイク\_配列\_を記述するためにオーディオドライバーで使用される ksk audio MIC 配列ジオメトリ構造を示しています。

```cpp
KSAUDIO_MIC_ARRAY_GEOMETRY mic_Array =
{
 0x100,// usVersion (1.0)
 KSMICARRAY_MICARRAYTYPE_LINEAR,// usMicArrayType
 7854,  // wVerticalAngleBegin (45 deg; PI/4 radians x 10000)
 -7854,  // wVerticalAngleEnd
 0, // lHorizontalAngleBegin
 0, // lHorizontalAngleEnd
 25, // usFrequencyBandLo in Hz
 19500, // usFrequencyBandHi in Hz
 2,  // usNumberOfMicrophones
 ar_mic_Coordinates // KsMicCoord
};
```

上記のコード例では、ar\_mic\_座標変数は ksk オーディオ\_マイク\_座標構造の配列であり、マイク配列内のマイクの座標が含まれています。

次のコード例では、前\_の\_コード例で説明したように、ar mic 座標配列を使用してマイク配列内のマイクの幾何学的な位置を記述する方法を示します。

```cpp
KsMicCoord ar_mic_Coordinates[] =
{
 // Array microphone 1
 {
  KSMICARRAY_MICTYPE_CARDIOID,// usType
  100, // wXCoord (mic elements are 200 mm apart)
  0,// wYCoord 
  0, // wZCoord 
  0,// wVerticalAngle
  0,// wHorizontalAngle
 },
 // Array microphone 2
 {
  KSMICARRAY_MICTYPE_CARDIOID,// usType
  -100, // wXCoord 
  0,// wYCoord 
  0, // wZCoord 
  0,// wVerticalAngle
  0,// wHorizontalAngle
 }
};
```

前のコード例では、マイク配列の各マイクに対して、有効な作業領域を示す垂直方向と水平方向の角度で、x-y 座標が指定されています。

Micarray MSVAD サンプルドライバーを変更して、仮想マイク配列の配列ジオメトリ情報を提供するには、次のタスクを実行する必要があります。

まず、Src\\Audio\\Msvad\\Micarray に移動し、mintopo .cpp ファイルを見つけます。 Mintopo .cpp のプロパティハンドラーセクションを編集して、KSAUDIO\_MIC\_配列\_の GEOMETRY 構造体にマイク配列に関する情報が含まれるようにします。 変更する必要があるコードの特定のセクションを次のコード例に示します。

```cpp
// Modify this portion of PropertyHandlerMicArrayGeometry
PKSAUDIO_MIC_ARRAY_GEOMETRY pMAG = (PKSAUDIO_MIC_ARRAY_GEOMETRY)PropertyRequest->Value;

// fill in mic array geometry fields
pMAG->usVersion = 0x0100;           // Version of Mic array specification (0x0100)
pMAG->usMicArrayType = (USHORT)KSMICARRAY_MICARRAYTYPE_LINEAR;        // Type of Mic Array
pMAG->wVerticalAngleBegin = -7854;  // Work Volume Vertical Angle Begin (-45 degrees)
pMAG->wVerticalAngleEnd   =  7854;  // Work Volume Vertical Angle End   (+45 degrees)
pMAG->wHorizontalAngleBegin = 0;    // Work Volume Horizontal Angle Begin
pMAG->wHorizontalAngleEnd   = 0;    // Work Volume Horizontal Angle End
pMAG->usFrequencyBandLo = 100;      // Low end of Freq Range
pMAG->usFrequencyBandHi = 8000;     // High end of Freq Range
 
pMAG->usNumberOfMicrophones = 2;    // Count of microphone coordinate structures to follow.

pMAG->KsMicCoord[0].usType = (USHORT)KSMICARRAY_MICTYPE_CARDIOID;          
pMAG->KsMicCoord[0].wXCoord = -100; // mic elements are 200 mm apart
pMAG->KsMicCoord[0].wYCoord = 0;         
pMAG->KsMicCoord[0].wZCoord = 0;         
pMAG->KsMicCoord[0].wVerticalAngle = 0;  
pMAG->KsMicCoord[0].wHorizontalAngle = 0;

pMAG->KsMicCoord[1].usType = (USHORT)KSMICARRAY_MICTYPE_CARDIOID;          
pMAG->KsMicCoord[1].wXCoord = 100;  // mic elements are 200 mm apart
pMAG->KsMicCoord[1].wYCoord = 0;         
pMAG->KsMicCoord[1].wZCoord = 0;         
pMAG->KsMicCoord[1].wVerticalAngle = 0;  
pMAG->KsMicCoord[1].wHorizontalAngle = 0;
```

前のコード例では、2つのマイク要素を持つ線形マイク配列に提供された情報を示しています。これらはそれぞれ cardioid 型で、配列の中心から 100 mm に位置しています。

2番目の変更については、「 [Msvad Micarray 用に変更](modified-inf-for-msvad-micarray.md)された inf」に示されているように Msvad ファイルを編集します。

ファイルの変更が完了したら、次の手順を実行して、マイク配列用のサンプルドライバーをビルドしてインストールします。

1.  作業する WDK ビルド環境を開始します。 たとえば、x86 の無料ビルド環境です。

2.  Src\\Audio\\Msvad フォルダーに移動します。

3.  [**ビルド**] コマンドを入力し、enter キーを押します。

4.  変更した Msvad ファイルを、ビルドプロセスによって作成された次のフォルダーにコピーします。

    Src\\Audio\\Msvad\\micarray\\objfre\_wlh\_x86\\i386

5.  手順 4. のフォルダーに、Vadarray. sys という名前のファイルが含まれていることを確認します。

6.  コントロールパネルを開き、[**ハードウェアの追加**] を使用して、サンプルドライバーを手動でインストールします。

7.  コントロールパネルの [**サウンド**] アプレットを開き、[**録音**] タブをクリックして、先ほどインストールした仮想マイクアレイが表示されることを確認します。

マイクアレイを検出するアプリケーションを開発する方法の詳細については、「 [Windows Vista のマイク配列を構築して使用する方法](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/MicArrays_guide.doc)」の付録 C を参照してください。

 

 




