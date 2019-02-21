---
title: SetupPreferredAudioDevices
description: SetupPreferredAudioDevices
ms.assetid: cc6b7da4-335d-4629-ba54-32aa32a1eb09
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1811c10c9ac649c7e58d5f7c7cd6b89946664d39
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535976"
---
# <a name="setuppreferredaudiodevices"></a>SetupPreferredAudioDevices


## <span id="ddk_setuppreferredaudiodevices_ks"></span><span id="DDK_SETUPPREFERREDAUDIODEVICES_KS"></span>


SetupPreferredAudioDevices キーワードは、デバイス、システムでは、1 つ含まれている場合、既定では、オーディオ システムができるようにするには、優先するオーディオ デバイスまたは複数のオーディオ デバイスを表します。 このキーワードは media クラスの特定と Microsoft Windows Millennium Edition または Windows 98、Microsoft Windows 2000、Windows XP、および Windows Vista でサポートされます。 SetupPreferredAudioDevicesis Windows 7 でサポートされていません。

オーディオ デバイスを作成するときに明示的にではなくアプリケーション プログラムが既定値を使用するよう選択 (または優先) デバイスはデバイスを指定します。 (例: の説明を表示、 [ **waveOutOpen** ](https://msdn.microsoft.com/library/windows/desktop/dd743866)と**DirectSoundCreate** Microsoft Windows SDK のドキュメント内の関数)。

オーディオのシステムの追跡、システム レジストリで、現在の優先オーディオ デバイス。 新しいオーディオ デバイスをインストールすることによって、システムをアップグレードすると、通常、デバイスをインストールする専用の INF ファイルは、優先するオーディオ デバイスとして、新しいデバイスを指定するレジストリを更新します。

SetupPreferredAudioDevices キーワードは、レジストリの更新のディレクティブを囲むことができます、**追加レジストリ セクション**(を参照してください[ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)) 用の INF ファイルのオーディオ デバイス。 このディレクティブは、次の形式です。

*reg rootkey*、 \[ *reg サブキー*\]SetupPreferredAudioDevices \[*フラグ*\]、 \[ *dword 値*\]

ディレクティブには、オーディオ システム サウンドの再生や録音、MIDI 音楽の再生の既定値として、デバイスのオーディオ機能を使用するように指示します。 サウンドとマルチ メディアのコントロール パネルの インストール後、これら 3 つの既定値が表示されます、**オーディオ**タブ。ユーザーは、既定のデバイスを変更するのにコントロール パネルを使用できます。

ディレクティブの*dword 値*パラメーター ディレクティブを有効にするには 0 以外の値にする必要がある DWORD 値を指定します。 この値が 0 の場合、ディレクティブは影響を与えません。 ため、Windows Me/98 は登録をサポートしない\_DWORD レジストリ データ型のただし、 *dword 値*は通常、4 バイト REG として表現\_の代わりに (たとえば、「01,00,00,00」として、DWORD としてバイナリの型"0x00000001") 代わりに。 *Dword 値*するには、ディレクティブの生のバイナリ形式でパラメーターを指定できます*フラグ*パラメーターを「1」(FLG\_ADDREG\_BINVALUETYPE)。

ディレクティブは、デバイスのドライバーがインストールされている時にも反映されます。 別のデバイスでは、新しいデバイスのインストール時に好みのデバイスの役割を占める、したがってこのロールからその他のデバイスを置き換えたり、好みのデバイスのロールを想定する新しいデバイスと、ディレクティブ。

アップグレードまたはインストールされているデバイスのドライバーを再インストール、サウンドの再生や録音、MIDI 音楽の再生、ユーザーの現在の優先-デバイスの選択を変更しないようにしたい場合があります。 場合は、設定、FLG\_ADDREG\_NOCLOBBER ビット、*フラグ*パラメーターをデバイスの初期インストールの場合にのみ有効にするディレクティブ。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次の例では、SetupPreferredAudioDevices キーワードを使用する方法を示す INF ファイルの一部を示します。

```inf
  AddReg = XYZ-Audio-Device.AddReg
  ...
  [XYZ-Audio-Device.AddReg]
  HKR,,SetupPreferredAudioDevices,3,01,00,00,00
```

例では、最後に、ディレクティブでは、「XYZ オーディオ デバイス」をという名前のデバイスは、優先するオーディオ デバイスで今すぐを指定します。 HKR は、レジストリでのオーディオ デバイスのルート キーです。 *フラグ*パラメーターは、ビットごとまたはの FLG は 3 に設定\_ADDREG\_BINVALUETYPE と FLG\_ADDREG\_NOCLOBBER します。 後者の場合で、デバイスが既にインストールされているし、そのドライバーをアップグレードしているだけで、上書きからのデバイスの既存の優先デバイス レジストリ エントリができないようにします。 ディレクティブの末尾にある 4 バイトでは、ディレクティブを有効にする必要が 0 以外の値を指定します。

Windows Vista では、あらゆるオーディオ エンドポイントで SetupPreferredAudioDevices キーワードの現在の実装でその*dword 値*奇数に設定を既定のデバイスとして設定できます。 適切なエンドポイントが既定のデバイスとして設定されていることを確認するには、関連するエンドポイントを含む KS フィルターが最後に公開されることを確認します。 これを行うため、AudioEndpointBuilder サービス ストアのプロパティおよび設定の既定のデバイスの設定に使用するアルゴリズムがあります。

 

 





