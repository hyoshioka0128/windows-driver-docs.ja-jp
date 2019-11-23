---
title: マルチチャンネル ノードの公開
description: マルチチャンネル ノードの公開
ms.assetid: 48ee3b33-fb97-4e71-bf6f-5dbdb76aa7f8
keywords:
- オーディオのプロパティ WDK、マルチチャネルノード
- WDM オーディオプロパティ WDK、マルチチャネルノード
- マルチチャネルノードの公開
- マルチチャネルノード WDK オーディオ
- ノード WDK オーディオ、マルチチャネル
- 最小ボリュームレベル WDK オーディオ
- 最大ボリュームレベル WDK オーディオ
- basic-サポートクエリ WDK オーディオ
- 範囲値 WDK オーディオ
- SndVol32 WDK オーディオ
- 複数チャネルのサポート WDK オーディオ
- スピーカー WDK オーディオ、マルチチャネルノード
- チャネルマルチチャネルサポート WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a85525db569f2121474bc85da28f1c01270e77e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833402"
---
# <a name="exposing-multichannel-nodes"></a>マルチチャンネル ノードの公開


## <span id="exposing_multichannel_nodes"></span><span id="EXPOSING_MULTICHANNEL_NODES"></span>


Windows XP より前のバージョンの Microsoft Windows では、WDM オーディオドライバーは、次の種類のマルチチャネルノードを簡単に公開できません。

[**KSNODETYPE\_ボリューム**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)

[**KSNODETYPE\_ミュート**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mute)

[**KSNODETYPE\_声調**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-tone)

特に、ノードに対してサポートされているチャネルの数を明示的に照会するメカニズムは存在しません。 この問題に対する回避策はありますが、欠点があります。 たとえば、クライアントは、 [**Ksk プロパティ\_AUDIO\_VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)プロパティを使用して、各チャネルのボリュームレベル ([**KSNODETYPE\_ボリューム**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)) に対して反復的にクエリを実行することができます。これにより、要求が、チャネルがこれ以上存在しないことを示すエラーを返します。 ただし、この手法では複数のクエリが必要であり、より新しいマルチチャネルオーディオデバイスの処理には効率が悪くなります。 Windows XP 以降のオペレーティングシステムでは、この制限は、次の2つのフラグビットを[**ksk\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_membersheader)の**Flags**メンバーに定義することによって解決されます。この構造は、プロパティハンドラーが基本サポートクエリに応答して出力します。

-   KSK プロパティ\_メンバー\_フラグ\_BASICSUPPORT\_マルチチャネル

    ノードでの基本サポートプロパティ要求では、ハンドラーはこのフラグビットを設定して、ノードがサポートしているチャネルの数を含む KSK プロパティ\_**Memberscount**メンバーが含まれることを示します。 Windows Vista 以降の Windows オペレーティングシステムでは、すべてのチャネルプロパティにこのフラグを設定する必要があります。

-   KSK プロパティ\_メンバー\_フラグ\_BASICSUPPORT\_UNIFORM

    ハンドラーは、このフラグビットと KSK プロパティ\_メンバーの間でビットごとの OR を実行し、1つのプロパティ値がノード内のすべてのチャネルで一様に適用されることを示す\_BASICSUPPORT\_マルチチャネルフラグビットを\_します。 たとえば、ハードウェアがすべてのチャネルに対して1つのボリュームレベルの制御のみを提供する場合、この制限を示すために、ボリュームノードの基本サポートハンドラーは、KSPROPERTY\_メンバー\_フラグ\_BASICSUPPORT\_UNIFORM flag を設定します。 このフラグが設定されていない場合、各チャネルのボリュームレベルは、他のチャネルのボリュームレベルとは別に制御できます。

    **   KSK**プロパティ\_メンバー\_フラグ\_basicsupport\_UNIFORM FLAG は、Windows Vista オペレーティングシステムでは使用されません。

     

Windows XP 以降のミニポートドライバーでは、マルチチャネルボリュームノードのプロパティハンドラーは、KSK プロパティ\_AUDIO\_VOLUMELEVEL クエリに応答して、\_BASICSUPPORT\_マルチチャネルビットに\_フラグを\_設定する必要があります。 ハンドラーは、1つの\_\_ノードによって公開されている各チャネルに対して1つずつ、\_長い**構造体**をステップ実行[ **\_、ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_long)の配列を返します。 各配列要素には、チャネルの最小ボリュームレベルと最大ボリュームレベル、および範囲内の連続する値間の差分が記述されます。 個々のチャネルに対して異なる範囲を指定して、一様でない範囲のチャネルを正しく公開できるようにすることができます。 たとえば、サブウーハーチャネルは、他のチャネルとは異なる範囲を持つ場合があります。

次のコード例では、一様でないプロパティ値を使用して、[オーディオプロパティの基本サポートクエリ](basic-support-queries-for-audio-properties.md)を処理する方法を示します。 次のコードの最初の行の変数 pDescription は、ハンドラーが基本サポート情報を書き込むデータバッファーの先頭にある[**Ksk プロパティ\_DESCRIPTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_description)構造体を指します。

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

次の図は、この例のデータバッファーのレイアウトを示しています。 PDescription、Pdescription、および pRange 各ポインターは、バッファー内のそれぞれのオフセットを指すように示されます。

![基本サポートクエリ用のデータバッファーのレイアウトを示す図](images/propdesc.png)

この例では、ハンドラーは**Memberscount**を**ulnumchannels**(チャネル数) に設定します。 範囲配列のサイズ (バイト単位) は、

**Memberssize** \* **memberssize**

この例では、KSK プロパティ\_メンバー\_フラグ\_BASICSUPPORT\_UNIFORM flag が設定されている場合、ハンドラーは、配列内のすべての ksproperty プロパティを同じ範囲に設定します。\_\_

トーンノードの[**Ksk プロパティ\_audio\_低音**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-bass)、 [**KSK プロパティ\_オーディオ\_高音**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-treble)、または[**KSK プロパティ\_オーディオ\_MID**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-mid)プロパティの基本サポートハンドラーは同様の方法で動作します。

マルチチャネルノードにブール型のチャネルごとのプロパティ値を持つプロパティがある場合、基本サポートハンドラーは、ステップ実行範囲配列の値を入力する必要があります。 この場合、ハンドラーは、次のコード例に示されている値にメンバーを設定します。 この種類のプロパティの2つの例は、ミュートノードの[**ksk プロパティ\_audio\_ミュート**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-mute)プロパティ、および声調ノードの[ **\_オーディオ\_低音\_ブースト**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-bass-boost)プロパティです。

次のコード例では、BOOL 型のチャネルごとのプロパティ値を持つプロパティの場合に、マルチチャネルノードの基本サポート要求を処理する方法を示します。

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

前のコード例では、FOR ループで 0 (0) と 1 (1) を使用して、チャネルごとの範囲の最小値と最大値を設定することに注意してください。 これは、' BOOL ' 型のチャネルごとのプロパティ値を使用してマルチチャネルノードを構成しているためです。

チャネルプロパティが一様である場合は、KSK プロパティ\_メンバー\_フラグ\_BASICSUPPORT\_UNIFORM FLAG、および KSK プロパティ\_メンバー\_フラグ\_BASICSUPPORT\_マルチチャネルフラグ、および pMembers-&gt;Flags メンバーに割り当てられた結果に対して、ビットごとの OR 演算を実行できます。 この値は、ハードウェアによって、ノード内のすべてのチャネルで同じプロパティ値が一様に適用されることを示すために使用されます。

KSK プロパティ\_メンバー\_フラグ\_UNIFORM と KSK プロパティ\_メンバー\_フラグを使用すると、チャネルをペアにグループ化して、チャネルのペアごとに個別のステレオボリュームノードを公開する必要がなくなります。これは、Windows Driver Kit (WDK) の Ac97 サンプルドライバーで行われます。\_ Windows XP より前のバージョンの Windows では、これらのフラグがサポートされていないため、ドライバーの基本サポートハンドラーは[Iportclsversion](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclsversion)インターフェイスを使用して Portcls のバージョンを照会し、これらのフラグを使用するかどうかを判断する必要があります。

(カーネルモード[WDMAud システムドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)の WDMAud の) トポロジパーサーは、WDM オーディオドライバーからオーディオデバイスのトポロジを取得します。 パーサーは、従来の Windows マルチメディア**ミキサー** API を使用して、そのデバイスを従来のミキサーデバイスとして公開します。 Windows XP 以降では、WDMAud は KSK プロパティ\_メンバー\_フラグ\_BASICSUPPORT\_マルチチャネルフラグを使用して、MIXERLINE 構造体の**Cchannels**メンバーで報告するチャネルの数を決定します。 さらに、ノードの基本サポートハンドラーで KSK プロパティ\_メンバー\_フラグ\_BASICSUPPORT\_UNIFORM flag が指定されている場合、WDMAud は対応する MIXERCONTROL 構造体の MIXERCONTROL\_CONTROLF\_UNIFORM フラグを設定します。 このフラグを使用すると、アプリケーションでは、各チャネルを個別に調整できるか、すべてのチャネルをマスタコントロールを通じて一様に調整できるかを判断できます。 MIXERCONTROL、MIXERLINE、および**ミキサ**API の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

Windows XP 以降では、次の図に示すように、SndVol32 volume control プログラム (「 [SysTray と SndVol32](systray-and-sndvol32.md)」を参照) によってマルチチャネルデバイスのコントロールが表示されます。

![[sndvol32 のボリュームコントロール] ダイアログボックスのスクリーンショット ](images/volctrl.png)

SndVol32 が3つを超えるチャネルを持つ行を検出すると、通常のパンコントロールは、前の図のメイン音量スライダーの上に表示される **[スピーカーの音量]** というラベルのボタンに置き換えられます。 **[スピーカー音量]** ボタンをクリックすると、次の図に示すように、特定の行のすべてのチャンネルのコントロールを表示するダイアログが表示されます。

![オーディオの詳細プロパティが表示された [スピーカー音量] ダイアログボックスのスクリーンショット](images/spkrvol.png)

**ミキサー** API はチャネルを番号で公開するため、Windows マルチメディアコントロールパネル (mmsys. cpl) の **[オーディオの詳細プロパティ**] ダイアログで現在選択されているスピーカーの構成からチャネル名を推測します。

たとえば、デバイスが1行に4つのチャンネルを公開し、ユーザーが "Quadraphonic 講演" を選択した場合、チャネル名は、前の図に示すように、"Left" (channel 0)、"Right" (channel 1)、"Back Left" (channel 2)、および "Back Right" (channel 3) になります。 スピーカーの構成を "サラウンドサウンドスピーカー" に変更すると、"左" (チャネル 0)、"右" (チャネル 1)、"フロントセンター" (チャネル 2)、および "バックセンター" (チャネル 3) のチャネルマッピングが発生します。

ドライバーレベルでは、KSK プロパティ\_AUDIO\_CHANNEL\_CONFIG プロパティでは、1つのマスク値が使用されています。\_スピーカー\_QUAD または KSPROPERTY\_スピーカー\_、quadraphonic またはサラウンドスピーカー構成を表します。 ヘッダーファイル Ksmedia. h は、これらの値を次のように定義します。

```cpp
  #define KSAUDIO_SPEAKER_QUAD      (SPEAKER_FRONT_LEFT | SPEAKER_FRONT_RIGHT | \
                                     SPEAKER_BACK_LEFT | SPEAKER_BACK_RIGHT)

  #define KSAUDIO_SPEAKER_SURROUND  (SPEAKER_FRONT_LEFT | SPEAKER_FRONT_RIGHT | \
                                     SPEAKER_FRONT_CENTER | SPEAKER_BACK_CENTER)
```

どちらのマスクにも、4つのチャンネルのスピーカーの位置を指定する4つのビットが含まれます。 どちらの場合も、KSK プロパティ\_AUDIO\_VOLUMELEVEL プロパティは、チャネル0、1、2、3と同じ4つのチャネルを識別します。

ノードの基本サポートハンドラーが KSK プロパティ\_メンバー\_フラグ\_BASICSUPPORT\_UNIFORM flag bit を設定した場合、 **[スピーカーの音量]** ダイアログに表示されるスライダーは、任意の1つのスライダーに加えられた変更と連動して移動します。

 

 




