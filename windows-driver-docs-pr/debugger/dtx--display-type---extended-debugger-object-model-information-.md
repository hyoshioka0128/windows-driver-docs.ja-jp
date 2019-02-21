---
title: dtx (表示の種類 - デバッガー オブジェクト モデル情報の拡張)
description: Dtx コマンドは、デバッガーのオブジェクト モデルを使用してシンボリック拡張の型情報を表示します。 Dtx コマンドは、dt (表示の種類) コマンドに似ています。
ms.assetid: 758D752E-65A0-4F1D-BB56-06E4ECEC6D48
keywords:
- dtx (表示の種類 - デバッガー オブジェクト モデル情報の拡張) Windows のデバッグ
ms.date: 09/17/2017
topic_type:
- apiref
api_name:
- dtx (Display Type - Extended Debugger Object Model Information)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 148b1f9be720fcdfa9fbe669c64778803b49659f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531842"
---
# <a name="span-iddebuggerdtxdisplaytype-extendeddebuggerobjectmodelinformationspandtx-display-type---extended-debugger-object-model-information"></a><span id="debugger.dtx__display_type_-_extended_debugger_object_model_information_"></span>dtx (表示の種類 - デバッガー オブジェクト モデル情報の拡張)


Dtx コマンドは、デバッガーのオブジェクト モデルを使用してシンボリック拡張の型情報を表示します。 Dtx コマンドと似ています、 [ **dt (表示の種類)** ](dt--display-type-.md)コマンド。

```dbgcmd
dtx -DisplayOpts [Module!]Name Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="________DisplayOpts_______"></span><span id="________displayopts_______"></span><span id="________DISPLAYOPTS_______"></span> **DisplayOpts**   
出力の表示方法を変更するのにには、次のオプションのフラグを使用します。

*-* 表示配列の要素がそのインデックスを持つ新しい行にします。

*-r \[n\]* 再帰的には、サブタイプ (フィールド) を最大ダンプ*n*レベル。

*-h* dtx コマンドのコマンド ライン ヘルプを表示します。

<span id="Module______________"></span><span id="module______________"></span><span id="MODULE______________"></span>**モジュール。**   
感嘆符の後に、この構造を定義するモジュールを指定する、省略可能なパラメーター。 含める必要がある場合は、ローカル変数またはグローバル変数または型と同じ名前の型がある、*モジュール*グローバル変数を指定する名前。

<span id="________Name_______"></span><span id="________name_______"></span><span id="________NAME_______"></span> **名**   
型名またはグローバル シンボル。

<span id="________Address_______"></span><span id="________address_______"></span><span id="________ADDRESS_______"></span> **アドレス**   
型を含むメモリ アドレス。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

次の例では、dtx コマンドを使用する方法を示します。

シンボリック拡張の型情報を表示するのにには、アドレスと名前を使用します。

```dbgcmd
0: kd> dtx nt!_EPROCESS ffffb607560b56c0
(*((nt!_EPROCESS *)0xffffb607560b56c0))                 [Type: _EPROCESS]
    [+0x000] Pcb              [Type: _KPROCESS]
    [+0x2d8] ProcessLock      [Type: _EX_PUSH_LOCK]
    [+0x2e0] RundownProtect   [Type: _EX_RUNDOWN_REF]
    [+0x2e8] UniqueProcessId  : 0x4 [Type: void *]
    [+0x2f0] ActiveProcessLinks [Type: _LIST_ENTRY]
```

-R 再帰のオプションを使用して追加の情報を表示します。

```dbgcmd
0: kd> dtx -r2 HdAudio!CAzMixertopoMiniport fffff806`d24992b8
(*((HdAudio!CAzMixertopoMiniport *)0xfffff806d24992b8))                 [Type: CAzMixertopoMiniport]
    [+0x018] m_lRefCount      : -766760880 [Type: long]
    [+0x020] m_pUnknownOuter  : 0xfffff806d24dbc40 [Type: IUnknown *]
    [+0x028] m_FilterDesc     [Type: PCFILTER_DESCRIPTOR]
        [+0x000] Version          : 0xd24c2890 [Type: unsigned long]
        [+0x008] AutomationTable  : 0xfffff806d24c2780 [Type: PCAUTOMATION_TABLE *]
            [+0x000] PropertyItemSize : 0x245c8948 [Type: unsigned long]
            [+0x004] PropertyCount    : 0x6c894808 [Type: unsigned long]
            [+0x008] Properties       : 0x5718247489481024 [Type: PCPROPERTY_ITEM *]
            [+0x010] MethodItemSize   : 0x55415441 [Type: unsigned long]
            [+0x014] MethodCount      : 0x57415641 [Type: unsigned long]
            [+0x018] Methods          : 0x4ce4334540ec8348 [Type: PCMETHOD_ITEM *]
            [+0x020] EventItemSize    : 0x8b41f18b [Type: unsigned long]
            [+0x024] EventCount       : 0xd8b48f4 [Type: unsigned long]
            [+0x028] Events           : 0x7d2d8d4cfffdf854 [Type: PCEVENT_ITEM *]
            [+0x030] Reserved         : 0x66fffd79 [Type: unsigned long]
        [+0x010] PinSize          : 0xd24aa9b0 [Type: unsigned long]
        [+0x014] PinCount         : 0xfffff806 [Type: unsigned long]
        [+0x018] Pins             : 0xfffff806d24aa740 [Type: PCPIN_DESCRIPTOR *]
            [+0x000] MaxGlobalInstanceCount : 0x57555340 [Type: unsigned long]
            [+0x004] MaxFilterInstanceCount : 0x83485741 [Type: unsigned long]
            [+0x008] MinFilterInstanceCount : 0x8b4848ec [Type: unsigned long]
            [+0x010] AutomationTable  : 0xa5158b48ed33c000 [Type: PCAUTOMATION_TABLE *]
            [+0x018] KsPinDescriptor  [Type: KSPIN_DESCRIPTOR]
```

ヒント:使用して、 [ **(シンボルを調べる) x** ](x--examine-symbols-.md)目的の項目のアドレスを表示するコマンド。

```dbgcmd
0: kd> x /d HdAudio!CazMixertopoMiniport*
...
fffff806`d24992b8 HdAudio!CAzMixertopoMiniport::`vftable' = <no type information>
...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**dt (表示の種類)**](dt--display-type-.md)

 

 






