---
title: マイク配列 Geometry プロパティ
description: マイク配列 Geometry プロパティ
ms.assetid: 7f280677-f86d-4687-b992-e2580046bd57
keywords:
- mic の配列の WDK オーディオ
- geometry 記述子 WDK オーディオ
- マイク配列 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51a9ca3ddc96b3ece4005691749373dfc0f9d2d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539155"
---
# <a name="microphone-array-geometry-property"></a>マイク配列 Geometry プロパティ


Windows Vista 以降では、マイク配列のサポートが提供されます。 ほとんどの場合、ラップトップ コンピューターやモニターに埋め込まれている 1 つのマイクをキャプチャしませんサウンドも非常にします。 マイクの配列が優れてをサウンドのソースを特定し、アンビエント ノイズとリバーブを拒否します。 [ **KSPROPERTY\_オーディオ\_MIC\_配列\_GEOMETRY** ](https://msdn.microsoft.com/library/windows/hardware/ff537289)プロパティがマイク配列のジオメトリを指定します。 プロパティの値[ **KSAUDIO\_MIC\_配列\_GEOMETRY**](https://msdn.microsoft.com/library/windows/hardware/ff537087)配列型 (線形、平面、)、マイク、配列内の数を記述し、その他の機能です。

このトピックでは、外部 USB マイクが配列を使用できます Windows Vista で提供されているマイク配列のサポートについて説明します。 外部 USB マイク配列は、ジオメトリとその配列への応答の他の機能を説明するために必要なパラメーターを指定する必要があります、**取得\_MEM**要求。

USB のマイク配列は、ジオメトリの情報を提供するのに標準書式指定を使用します。 Windows Vista の USB オーディオ クラス ドライバーは、ジオメトリの情報を読み取る際に、同じ形式を使用する必要があります。 標準の形式の詳細については、[マイク配列 Geometry 記述子形式](microphone-array-geometry-descriptor-format.md)を参照してください。

アプリケーションが呼び出すことができます[IPart::GetSubType](https://go.microsoft.com/fwlink/p/?linkid=143726)ジャック、ジャックに接続されたデバイスがマイク配列かどうかを決定に関する情報を取得します。 **IPart::GetSubType**入力ジャックに接続の種類を表す暗証番号 (pin) カテゴリの GUID を返します。 接続されているデバイスのマイク配列が返される GUID は KSNODETYPE に等しく\_マイク\_配列。 アプリケーションは、マイク配列を間違ったジャックに接続したかどうかを判断することができます。 後者のシナリオでは、返された pin のカテゴリの GUID は、別のデバイスのいずれかまたはマイクのジャックに接続されたデバイスがないことを示します。 暗証番号 (pin) カテゴリの Guid の詳細については、[Pin Category プロパティ](pin-category-property.md)を参照してください。

アプリケーションが適切な入力ジャックに接続されているマイク配列を検出した後、次の手順では、配列のジオメトリを決定します。 次の 3 つの基本的なジオメトリがある:*線形*、*平面*、および*3 次元 (3 D)* します。 ジオメトリの情報には、周波数の範囲と各マイクの x、y、z 座標などの詳細情報も提供します。

次のコード例に示します、KSAUDIO\_MIC\_配列\_オーディオ ドライバーを使用して外部 USB マイク配列を記述する GEOMETRY 構造体。

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

上記のコード例で、ar\_mic\_座標の変数が配列の KSAUDIO\_マイク\_座標の構造とそのマイク配列のマイクの座標が含まれています。

次のコード例は、ar\_mic\_Coordinates 配列は、上記のコード例」の説明に従って、マイク、マイク配列内のジオメトリの場所を記述するために使用します。

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

上記のコード例では、垂直および水平方向の角度、効果的な作業領域を記述すると共に、マイク配列内の各マイクの x、y、z 座標が与えられます。

仮想のマイク配列の配列のジオメトリの情報を提供する Micarray MSVAD サンプル ドライバーを変更するには、次のタスクを実行する必要があります。

まず、Src に移動します\\オーディオ\\Msvad\\Micarray Mintopo.cpp ファイルを見つけます。 Mintopo.cpp プロパティ ハンドラー セクションを編集できるように、KSAUDIO\_MIC\_配列\_GEOMETRY 構造にはについてには、マイク配列が含まれています。 変更する必要がありますコードの特定のセクションは、次のコード例に示されます。

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

上記のコード例がそれぞれ cardioid 型であり、配列の中心から 100 mm にある 2 つのマイク要素を線形のマイク配列の指定された情報が表示されます。

2 番目の変更のようにに Msvad.inf ファイルを編集[MSVAD Micarray の変更の INF](modified-inf-for-msvad-micarray.md)します。

ファイルの変更を完了すると、ビルドし、マイク配列のサンプル ドライバーをインストールするには、次の手順を完了します。

1.  作業する WDK ビルド環境を起動します。 たとえば、x86 ビルド環境。

2.  Src に移動します\\オーディオ\\Msvad フォルダー。

3.  型、**ビルド**コマンドを使用し、Enter キーを押します。

4.  ビルド プロセスによって作成された次のフォルダーに変更した Msvad.inf ファイルをコピーします。

    Src\\オーディオ\\Msvad\\Micarray\\objfre\_wlh\_x86\\i386

5.  手順 4. でフォルダーが Vadarray.sys という名前のファイルが含まれていることを確認します。

6.  コントロール パネルを開きを使用して、**ハードウェアの追加**サンプル ドライバーを手動でインストールします。

7.  開く、**サウンド**アプレット コントロール パネル をクリックして、**記録**配列だけをインストールする仮想マイクを表示できることを確認するには、タブ。

マイクのアレイを検出するアプリケーションを開発する方法については、付録 C を参照してください。[方法の構築および Windows Vista のマイク配列を使用して](https://go.microsoft.com/fwlink/p/?linkid=306613)します。

 

 




