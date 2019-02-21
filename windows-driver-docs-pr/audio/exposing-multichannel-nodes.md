---
title: マルチ チャネルのノードを公開します。
description: マルチ チャネルのノードを公開します。
ms.assetid: 48ee3b33-fb97-4e71-bf6f-5dbdb76aa7f8
keywords:
- WDK、マルチ チャネルのノードのオーディオのプロパティ
- WDM オーディオ プロパティ WDK、マルチ チャネルのノード
- マルチ チャネルのノードを公開します。
- マルチ チャネルのノードの WDK オーディオ
- ノードの WDK オーディオ、マルチ チャネル
- 最小ボリューム レベルの WDK オーディオ
- 最大ボリューム レベルの WDK オーディオ
- basic - クエリ WDK オーディオをサポート
- 範囲値の WDK オーディオ
- SndVol32 WDK オーディオ
- 複数のチャネル サポート WDK オーディオ
- スピーカー WDK のオーディオ、マルチ チャネルのノード
- WDK のオーディオをマルチ チャネルのサポート チャネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b6d4939617eb3deca96f9e40cd68fbf85005043
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549153"
---
# <a name="exposing-multichannel-nodes"></a>マルチ チャネルのノードを公開します。


## <span id="exposing_multichannel_nodes"></span><span id="EXPOSING_MULTICHANNEL_NODES"></span>


Windows XP より前の Microsoft Windows のバージョンでは、WDM オーディオ ドライバーには、次の種類のマルチ チャネルのノードを公開する簡単な手段がありません。

[**KSNODETYPE\_ボリューム**](https://msdn.microsoft.com/library/windows/hardware/ff537208)

[**KSNODETYPE\_ミュート**](https://msdn.microsoft.com/library/windows/hardware/ff537178)

[**KSNODETYPE\_トーン**](https://msdn.microsoft.com/library/windows/hardware/ff537205)

具体的には、明示的にサポートしているチャネルの数のノードを照会するためのメカニズムは存在しません。 この問題の回避策がありますが、欠点があります。 たとえば、クライアントが使用できます、 [ **KSPROPERTY\_オーディオ\_VOLUMELEVEL** ](https://msdn.microsoft.com/library/windows/hardware/ff537309)繰り返し、[ボリューム] ノードを照会するプロパティ ([**KSNODETYPE\_ボリューム**](https://msdn.microsoft.com/library/windows/hardware/ff537208)) - 各チャネルのボリューム レベル 0、1、およびようになって要求がチャネルもないことを示すエラーを返すまでは存在します。 ただし、この方法は複数のクエリを必要とされ、新しいマルチ チャンネル オーディオ デバイスを処理するために非常に効率ではありません。 Windows XP およびそれ以降のオペレーティング システムでは、この制限は 2 つの追加のフラグのビットを定義することで解決、**フラグ**のメンバー、 [ **KSPROPERTY\_MEMBERSHEADER**](https://msdn.microsoft.com/library/windows/hardware/ff565189)構造体は、プロパティ ハンドラーが basic サポート クエリに対する応答の出力します。

-   KSPROPERTY\_メンバー\_フラグ\_BASICSUPPORT\_マルチ チャネル

    ハンドラーが示すためにこのフラグのビットを設定するノードで、basic サポート プロパティ要求中に、 **MembersCount** KSPROPERTY のメンバー\_MEMBERSHEADER にはノードがサポートするチャネルの数が含まれています。 Windows Vista と以降の Windows オペレーティング システムでは、すべてのチャネル プロパティのこのフラグを設定する必要があります。

-   KSPROPERTY\_メンバー\_フラグ\_BASICSUPPORT\_UNIFORM

    ハンドラーは、このフラグのビットと、KSPROPERTY 間でビットごとの OR を実行します\_メンバー\_フラグ\_BASICSUPPORT\_をすべて 1 つのプロパティの値が一様に適用されることを示すために、マルチ チャネルのフラグ ビット。ノード内のチャネル。 たとえば、ハードウェアでは、すべてのチャネルの 1 つのボリューム レベル コントロールのみを提供する場合、[ボリューム] ノードの basic サポート ハンドラーが設定、KSPROPERTY\_メンバー\_フラグ\_BASICSUPPORT\_フラグを統一されました。この制限を示します。 このフラグが設定されていない場合は、他のチャネルのボリューム レベルとは無関係に各チャネルのボリューム レベルを制御できます。

    **注**   、KSPROPERTY\_メンバー\_フラグ\_BASICSUPPORT\_UNIFORM フラグは、Windows Vista オペレーティング システムでは使用されません。

     

Windows XP 以降のミニポート ドライバーでマルチ チャネルのボリュームのノードのプロパティのハンドラーが、KSPROPERTY を設定します\_メンバー\_フラグ\_BASICSUPPORT\_KSPROPERTYへの応答でマルチチャネルがビット。\_オーディオ\_VOLUMELEVEL basic サポート クエリ。 ハンドラーの配列を返します[ **KSPROPERTY\_ステッピング\_長い**](https://msdn.microsoft.com/library/windows/hardware/ff565631)構造--ノード セットによって公開される各チャネルに 1 つずつ**MembersSize**に**sizeof**(KSPROPERTY\_ステッピング\_長い)。 配列の各要素には、チャネルの最小値と最大のボリューム レベルと連続する値の範囲の間のデルタがについて説明します。 一様でない範囲を使用したチャネルを正しく公開できるように、各個々 のチャネルに対して異なる範囲を指定できます。 たとえば、サブウーファー チャネルには、他のチャネルとは異なる範囲があります。

次のコード例を処理する方法を示しています、[オーディオのプロパティのクエリを basic サポート](basic-support-queries-for-audio-properties.md)一様でないプロパティ値を使用します。 ポインターの下にコードの最初の行で変数 pDescription、 [ **KSPROPERTY\_説明**](https://msdn.microsoft.com/library/windows/hardware/ff565132)構造のハンドラーが書き込む先のデータ バッファーの先頭に、basic サポート情報:

```cpp
  //
  // Fill in the members header.
  //
  PKSPROPERTY_MEMBERSHEADER pMembers = PKSPROPERTY_MEMBERSHEADER(pDescription + 1);

  pMembers->MembersFlags = KSPROPERTY_MEMBER_STEPPEDRANGES;
  pMembers->MembersSize = sizeof(KSPROPERTY_STEPPING_LONG);
  pMembers->MembersCount = ulNumChannels;
  pMembers->Flags = KSPROPERTY_MEMBER_FLAG_BASICSUPPORT_MULTICHANNEL;

  //
  // Fill in the stepped range with the driver default.
  //
  PKSPROPERTY_STEPPING_LONG pRange = PKSPROPERTY_STEPPING_LONG(pMembers + 1);
  pRange->Reserved = 0;

  for (ULONG i=0; i<ulNumChannels; i++)
  {
      pRange[i].Bounds.SignedMinimum = ulChannelMin[i];
      pRange[i].Bounds.SignedMaximum = ulChannelMax[i];
      pRange[i].SteppingDelta = ChannelStepping[i];
  }

  pPropertyRequest->ValueSize = sizeof(KSPROPERTY_DESCRIPTION) +
                                sizeof(KSPROPERTY_MEMBERSHEADER) + 
                                ulNumChannels * sizeof(KSPROPERTY_STEPPING_LONG);
```

次の図は、この例のデータ バッファーのレイアウトを示します。 バッファー内のそれぞれのオフセットを指す pDescription、pMembers、および pRange ポインターが表示されます。

![basic サポート クエリ用のデータ バッファーのレイアウトを示す図](images/propdesc.png)

この例で、ハンドラーが設定**MembersCount**に**ulNumChannels**チャネルの数。 範囲の配列のバイト サイズします。

**MembersSize** \* **MembersCount**

KSPROPERTY ことに注意してください\_メンバー\_フラグ\_BASICSUPPORT\_UNIFORM フラグは、この例では設定された、ハンドラーが設定はすべて、KSPROPERTY の\_ステッピング\_内の時間構造体同じ範囲の配列。

トーン ノードの基本サポート ハンドラー [ **KSPROPERTY\_オーディオ\_低音**](https://msdn.microsoft.com/library/windows/hardware/ff537242)、 [ **KSPROPERTY\_オーディオ\_音**](https://msdn.microsoft.com/library/windows/hardware/ff537308)、または[ **KSPROPERTY\_オーディオ\_MID** ](https://msdn.microsoft.com/library/windows/hardware/ff537290)プロパティは、同様の方法で動作します。

マルチ チャネルのノードに BOOL 型のチャネルごとのプロパティ値を持つプロパティがある場合は、basic サポート ハンドラー ステップ実行範囲の配列の値を入力する必要があります。 この場合、ハンドラーは、次のコード例に示す値をメンバーを設定します。 この種類のプロパティの 2 つの例は、 [ **KSPROPERTY\_オーディオ\_ミュート**](https://msdn.microsoft.com/library/windows/hardware/ff537293)ミュート ノードのプロパティと[ **KSPROPERTY\_オーディオ\_低音\_BOOST** ](https://msdn.microsoft.com/library/windows/hardware/ff537245)トーン ノードのプロパティ。

次のコード例では、BOOL 型のチャネルごとのプロパティの値のプロパティの場合、マルチ チャネルのノードの基本サポート要求を処理する方法を示します。

```cpp
  //
  // Fill in the members header.
  //
  PKSPROPERTY_MEMBERSHEADER pMembers = PKSPROPERTY_MEMBERSHEADER(pDescription + 1);

  pMembers->MembersFlags = KSPROPERTY_MEMBER_STEPPEDRANGES;
  pMembers->MembersSize = sizeof (KSPROPERTY_STEPPING_LONG);
  pMembers->MembersCount = ulNumChannels;
  pMembers->Flags = KSPROPERTY_MEMBER_FLAG_BASICSUPPORT_MULTICHANNEL;

  pPropertyRequest->ValueSize = sizeof(KSPROPERTY_DESCRIPTION) +
                                sizeof(KSPROPERTY_MEMBERSHEADER) + 
                                ulNumChannels * sizeof(KSPROPERTY_STEPPING_LONG);

  //
  // Fill in the stepped range with values in FOR loop.
  //
  PKSPROPERTY_STEPPING_LONG pRange = PKSPROPERTY_STEPPING_LONG(pMembers + 1);
  pRange->Reserved = 0;

  for (ULONG i=0; i<ulNumChannels; i++)
  {
      pRange[i].Bounds.SignedMinimum = 0;
      pRange[i].Bounds.SignedMaximum = 1;
      pRange[i].SteppingDelta = 1;
  }
```

上記のコード例で、FOR ループではゼロ (0) と、1 つのチャネルごとの範囲の最小値と最大値を設定することを確認します。 これは、BOOL 型のチャネルごとのプロパティ値を持つマルチ チャネルのノードを構成していますので。

KSPROPERTY 間でビットごとの OR 演算を実行できるチャネルのプロパティが統一された場合は、\_メンバー\_フラグ\_BASICSUPPORT\_UNIFORM フラグと、KSPROPERTY\_メンバー\_フラグ\_BASICSUPPORT\_マルチ チャネルのフラグと pMembers - に割り当てられている結果&gt;フラグ メンバー。 この値をハードウェア適用されるプロパティ値が同じ一様に、ノードのすべてのチャネルで示すために使用されます。

KSPROPERTY を使用して\_メンバー\_フラグ\_一様と KSPROPERTY\_メンバー\_フラグ\_マルチ チャネルのフラグをペアにチャンネルをグループ化し、個別に公開する必要はありませんWindows Driver Kit (WDK) で Ac97 サンプル ドライバーで行われるよう、チャネルの各ペアのステレオ ボリューム ノードです。 Windows のバージョン以前 Windows XP よりはサポートされないためこれらのフラグ、basic サポートのハンドラーには、ドライバーを使用する必要があります、 [IPortClsVersion](https://msdn.microsoft.com/library/windows/hardware/ff536877) Portcls.sys バージョンを使用するかどうかを判断するためのクエリへのインターフェイスこれらのフラグ。

トポロジのパーサー (カーネル モードで[WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)Wdmaud.sys) WDM、オーディオ ドライバーから、オーディオ デバイスのトポロジを取得します。 パーサーが従来の Windows のマルチ メディアを使用して従来のミキサー デバイスとそのデバイスを公開する**ミキサー** API。 WDMAud が、KSPROPERTY を使用して Windows XP 以降では、\_メンバー\_フラグ\_BASICSUPPORT\_でレポートへのチャネルの数を決定するフラグをマルチ チャネル、 **cChannels**MIXERLINE 構造体のメンバーです。 さらに、ノードの基本サポート場合ハンドラーを指定、KSPROPERTY\_メンバー\_フラグ\_BASICSUPPORT\_UNIFORM フラグは、WDMAud 設定、MIXERCONTROL\_CONTROLF\_対応する MIXERCONTROL 構造で統一されたフラグです。 このフラグを使用アプリケーションは、各チャネルを個別に調整できるかどうか、またはマスター コントロールを一様にすべてのチャネルを確認できます。 MIXERCONTROL、MIXERLINE の詳細については、**ミキサー** API、Microsoft Windows SDK のドキュメントを参照してください。

Windows XP 以降では、SndVol32 ボリューム コントロールのプログラム (を参照してください[システム トレイと SndVol32](systray-and-sndvol32.md)) 次の図に示すように、マルチ デバイス用のコントロールが表示されます。

![sndvol32 ボリューム コントロール ダイアログ ボックスのスクリーン ショット ](images/volctrl.png)

というラベルのボタンを置き換えます SndVol32 が 3 つ以上のチャネルを持つ行を検出した場合、通常のパン コントロール**スピーカーの音量**、前の図にメイン音量スライダー上に表示されます。 クリックすると、**スピーカーの音量**ボタンは、次の図に示すように、特定の行のチャネルのすべてのコントロールを表示するダイアログが表示されます。

![高度なオーディオのプロパティを持つ、スピーカーの音量のダイアログ ボックスのスクリーン ショット](images/spkrvol.png)

**ミキサー**番号によってチャネルが API で公開、スピーカーの構成で現在選択されているチャネル名を推測、**オーディオの詳細プロパティ**Windows のダイアログマルチ メディア コントロール パネル (Mmsys.cpl)。

たとえば、行に 4 つのチャネルを公開するデバイスとユーザーが「4 チャンネル方式のスピーカー」を選択、チャネル名は、その前の図に示すように"Left"(チャネル 0)、"Right"(チャネル 1)、「戻る"(チャネル 2)、左右」戻る"(チャネル 3) になります。 スピーカーの構成を「サラウンド サウンド スピーカー」を変更すると、"Left"(チャネル 0)、"Right"(チャネル 1)、"前面 Center"(チャネル 2)、および"戻る Center"(チャネル 3) のチャネル マッピングが発生します。

ドライバー レベルで、KSPROPERTY\_オーディオ\_チャネル\_KSAUDIO のマスクの値を使用する構成プロパティ\_スピーカー\_クアッドまたは KSAUDIO\_スピーカー\_を囲む4 チャンネル方式またはサラウンド スピーカー構成をそれぞれ表します。 ヘッダー ファイル Ksmedia.h では、次のように、これらの値を定義します。

```cpp
  #define KSAUDIO_SPEAKER_QUAD      (SPEAKER_FRONT_LEFT | SPEAKER_FRONT_RIGHT | \
                                     SPEAKER_BACK_LEFT | SPEAKER_BACK_RIGHT)

  #define KSAUDIO_SPEAKER_SURROUND  (SPEAKER_FRONT_LEFT | SPEAKER_FRONT_RIGHT | \
                                     SPEAKER_FRONT_CENTER | SPEAKER_BACK_CENTER)
```

いずれかのマスクには、4 つのスピーカー位置を指定する 4 つのビットが含まれています。 どちらの場合、KSPROPERTY\_オーディオ\_VOLUMELEVEL プロパティが 0、1、2、3、およびチャネルとして同じこれら 4 つのチャンネルをそれぞれ識別します。

ハンドラーが、KSPROPERTY を設定する場合は、ノードの基本サポート\_メンバー\_フラグ\_BASICSUPPORT\_UNIFORM フラグのビットに示すように、スライダー、**スピーカーの音量**を調和よくダイアログの移動で任意の 1 つのスライダーに加えられた変更します。

 

 




