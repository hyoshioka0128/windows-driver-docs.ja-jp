---
title: DirectSound ハードウェア アクセラレータと SRC スライダー
description: DirectSound ハードウェア アクセラレータと SRC スライダー
ms.assetid: 40329177-b8d5-49a2-a1d3-6730a26b6e78
keywords:
- ハードウェア アクセラレータ WDK DirectSound、SRC スライダー
- スライダーの WDK オーディオ
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d0f62d71aaf7519a9266c260184e027fd3f99fb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574886"
---
# <a name="directsound-hardware-acceleration-and-src-sliders"></a>DirectSound ハードウェア アクセラレータと SRC スライダー


## <span id="directsound_hardware_acceleration_and_src_sliders"></span><span id="DIRECTSOUND_HARDWARE_ACCELERATION_AND_SRC_SLIDERS"></span>


Windows では、システム全体で DirectSound パフォーマンスを変更するためのグローバルのスライダー コントロールを提供します。 スライダーでは、ハードウェア高速化し、DirectSound のアプリケーションに利用可能なサンプル レートの変換 (SRC) の品質のレベルを制御します。 ハードウェア高速化と SRC スライダーに加えた変更は、ブート ups の間で永続的なは。

ハードウェア高速化と SRC 設定は、エンドユーザーが直接操作によってのみ変更できます。 アプリケーション プログラムから、ハードウェア アクセラレータまたは SRC 設定を変更する場合は API は有効ではありません。 この動作は、安定性が向上し、ソフトウェアが状態を削除できませんを再起動しなくても、オーディオ システムを配置することを防ぎます。

これらの設定では、DirectSound のアプリケーションのみに影響します。 WaveOut API が、DirectSound SRC スライダーの設定に関係なく最適な SRC 品質を常に使用されるに注意してください。 また、すべての最新バージョンの Windows で行うためで waveOut アプリケーションがオーディオ デバイスでハードウェア アクセラレータを使用した pin を使用できない、DirectSound ハードウェア アクセラレータ スライダーの設定による影響を受けません。 Windows のマルチ メディア waveOut API の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

Windows の検索は、DirectSound ハードウェア高速化して SRC スライダーを使用して、たとえば、次の手順します。

1.  コントロール パネルで、ダブルクリック、**サウンドとオーディオ デバイス**アイコン (または実行 mmsys.cpl)。

2.  **オーディオ** タブからデバイスを選択、**音の再生**一覧。

3.  **[詳細設定]** ボタンをクリックします。

4.  をクリックして、**パフォーマンス**タブ。

この時点では、ラベル付けされている 2 つのスライダーを表示する必要があります**ハードウェア アクセラレータ**と**レート変換の質をサンプル**します。

ハードウェア アクセラレータ スライダーが 4 つの設定範囲の**なし**(レベル 0)、左にある**完全**(レベル 3)、右側にします。 次の表では、これらの設定の意味を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">高速化のレベル</th>
<th align="left">設定の名前</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>エミュレーション</p></td>
<td align="left"><p>強制的にエミュレーション。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>基本</p></td>
<td align="left"><p>DirectSound セカンダリ バッファーのハードウェア アクセラレータを無効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>Standard</p></td>
<td align="left"><p>DirectSound セカンダリ バッファーのハードウェア アクセラレータをできますが、ベンダー固有のプロパティ セットの拡張機能を無効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>[完全]</p></td>
<td align="left"><p>DirectSound セカンダリ バッファーのハードウェア アクセラレータをでき、ベンダー固有のプロパティ セットの拡張機能を有効します。</p></td>
</tr>
</tbody>
</table>

 

<span id="Emulation_Setting"></span><span id="emulation_setting"></span><span id="EMULATION_SETTING"></span>**エミュレーションの設定**  
**エミュレーション**上の設定は、エミュレーション モードに DirectSound を強制します。 このモードでは、DirectSound のアプリケーションは、DirectSound のドライバーが存在しない場合と同様を実行します。 DirectSound によってユーザー モードでのすべての混在は行われます、waveOut API を通じて、結果のオーディオ データが再生されます。 結果は、待機時間で大きな数の増加では通常です。 

<span id="Basic_Setting"></span><span id="basic_setting"></span><span id="BASIC_SETTING"></span>**基本設定**  
**基本**設定は、DirectSound のセカンダリ バッファーのハードウェア アクセラレータを無効にします。 この設定は、は、DirectSound のすべてのアプリケーションは、ハードウェア アクセラレータが使用されているサウンド カードの機能に関係なく使用できないものとしてを実行します。 テスト中にこの設定は、DirectSound の高速化を持たないサウンド カードをエミュレートするために使用できます。 この設定など、高速化 DirectSound セカンダリ バッファーの図形がないと、OPL アダプターを使用したのと同じ効果は、**標準**設定します。 Windows Server 2003 で**基本的な**既定の設定です。

<span id="Standard_Setting"></span><span id="standard_setting"></span><span id="STANDARD_SETTING"></span>**標準の設定**  
**標準**設定は DirectSound セカンダリ バッファーのハードウェア アクセラレータをできますが、EAX (クリエイティブのテクノロジ環境オーディオ拡張) などのプロパティとして公開されているベンダー固有の拡張を無効にします設定、 **IKsPropertySet**インターフェイス (を参照してください[を公開するカスタム オーディオ プロパティを設定](exposing-custom-audio-property-sets.md))。 Windows 2000、**標準**設定が既定で選択されています。

<span id="Full_Setting"></span><span id="full_setting"></span><span id="FULL_SETTING"></span>**完全な設定**  
**完全**設定は、DirectSound のセカンダリ バッファーのアクセラレータを有効にします。 また、この設定により、プロパティのセットを通じて公開されているベンダー固有拡張機能の**IKsPropertySet**インターフェイス (を参照してください[を公開するカスタム オーディオ プロパティを設定](exposing-custom-audio-property-sets.md))。 **IKsPropertySet**拡張には EAX などのベンダー固有のハードウェアの機能強化が含まれます。 


ユーザーは、ハードウェア高速化、または既定値以外の値に SRC 設定を調整する場合、DirectSound は、既定ではなく、新しい設定を使用します。



 

 




