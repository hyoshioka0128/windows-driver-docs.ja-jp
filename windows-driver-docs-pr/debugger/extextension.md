---
title: ExtExtension
description: ExtExtension クラスは、EngExtCpp の拡張機能ライブラリを表す C++ クラスの基本クラスです。
ms.assetid: 9c6c4633-df49-4f49-8116-d680bb20c3f5
keywords:
- デバッグ ExtExtension Windows
topic_type:
- apiref
api_name:
- ExtExtension
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87ce030343c11671499718338cf6c8fe1f9de16f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529754"
---
# <a name="extextension"></a>ExtExtension


**ExtExtension**クラスは EngExtCpp の拡張機能ライブラリを表す C++ クラスの基本クラスです。

**ExtExtension**クラスにはサブクラスで使用できる次のメソッドが含まれています。

[**初期化します。**](https://msdn.microsoft.com/library/windows/hardware/ff550945)

[**初期化を解除します。**](https://msdn.microsoft.com/library/windows/hardware/ff558961)

[**OnSessionActive**](https://msdn.microsoft.com/library/windows/hardware/ff552312)

[**OnSessionInactive**](https://msdn.microsoft.com/library/windows/hardware/ff552318)

[**OnSessionAccessible**](https://msdn.microsoft.com/library/windows/hardware/ff552310)

[**OnSessionInaccessible**](https://msdn.microsoft.com/library/windows/hardware/ff552315)

**IsUserMode**

**IsKernelMode**

**IsLiveLocalUser**

**IsMachine32**

**IsCurMachine32**

**IsMachine64**

**IsCurMachine64**

**Is32On64**

**CanQueryVirtual**

**HasFullMemBasic**

**IsExtensionRemote**

**AreOutputCallbacksDmlAware**

**RequireUserMode**

**RequireKernelMode**

[**GetNumUnnamedArgs**](https://msdn.microsoft.com/library/windows/hardware/ff548001)

[**GetUnnamedArgStr**](https://msdn.microsoft.com/library/windows/hardware/ff549464)

[**GetUnnamedArgU64**](https://msdn.microsoft.com/library/windows/hardware/ff549465)

[**HasUnnamedArg**](https://msdn.microsoft.com/library/windows/hardware/ff549733)

[**GetArgStr**](https://msdn.microsoft.com/library/windows/hardware/ff545586)

[**GetArgU64**](https://msdn.microsoft.com/library/windows/hardware/ff545596)

[**HasArg**](https://msdn.microsoft.com/library/windows/hardware/ff549721)

[**HasCharArg**](https://msdn.microsoft.com/library/windows/hardware/ff549727)

[**SetUnnamedArg**](https://msdn.microsoft.com/library/windows/hardware/ff556876)

[**SetUnnamedArgStr**](https://msdn.microsoft.com/library/windows/hardware/ff556878)

[**SetUnnamedArgU64**](https://msdn.microsoft.com/library/windows/hardware/ff556879)

[**SetArg**](https://msdn.microsoft.com/library/windows/hardware/ff556614)

[**SetArgStr**](https://msdn.microsoft.com/library/windows/hardware/ff556618)

[**SetArgU64**](https://msdn.microsoft.com/library/windows/hardware/ff556622)

[**GetRawArgStr**](https://msdn.microsoft.com/library/windows/hardware/ff548226)

**GetRawArgCopy**

**アウト**

**警告を表示します。**

**エラー**

**動詞**

**Dml**

**DmlWarn**

**DmlErr**

**DmlVerb**

**DmlCmdLink**

**DmlCmdExec**

**RefreshOutputCallbackFlags**

**WrapLine**

**OutWrapStr**

**OutWrapVa**

**OutWrap**

**DemandWrap**

**AllowWrap**

**TestWrap**

**RequestCircleString**

**CopyCircleString**

**PrintCircleStringVa**

**PrintCircleString**

**SetAppendBuffer**

**AppendBufferString**

**AppendStringVa**

**AppendString**

**IsAppendStart**

**SetCallStatus**

**GetCachedSymbolTypeId**

**GetCachedFieldOffset**

**GetCachedFieldOffset**

**AddCachedSymbolInfo**

**GetExpr64**

**GetExprU64**

**GetExprS64**

**ThrowCommandHelp**

**ThrowInterrupt**

**ThrowOutOfMemory**

**ThrowContinueSearch**

**ThrowReloadExtension**

**ThrowInvalidArg**

**ThrowRemote**

**ThrowStatus**

**ThrowLastError**

**ExtExtension**クラスには、サブクラスで使用できる次のフィールドも含まれています。

```cpp
class ExtExtension
{
public:
    USHORT  m_ExtMajorVersion;
    USHORT  m_ExtMinorVersion;
    ULONG  m_ExtInitFlags;
    ExtKnownStruct *  m_KnownStructs;
    ExtProvidedValue *  m_ProvidedValues;
    ExtCheckedPointer<IDebugAdvanced>  m_Advanced;
    ExtCheckedPointer<IDebugClient>  m_Client;
    ExtCheckedPointer<IDebugControl>  m_Control;
    ExtCheckedPointer<IDebugDataSpaces>  m_Data;
    ExtCheckedPointer<IDebugRegisters>  m_Registers;
    ExtCheckedPointer<IDebugSymbols>  m_Symbols;
    ExtCheckedPointer<IDebugSystemObjects>  m_System;
    ExtCheckedPointer<IDebugAdvanced2>  m_Advanced2;
    ExtCheckedPointer<IDebugAdvanced3>  m_Advanced3;
    ExtCheckedPointer<IDebugClient2>  m_Client2;
    ExtCheckedPointer<IDebugClient3>  m_Client3;
    ExtCheckedPointer<IDebugClient4>  m_Client4;
    ExtCheckedPointer<IDebugClient5>  m_Client5;
    ExtCheckedPointer<IDebugControl2>  m_Control2;
    ExtCheckedPointer<IDebugControl3>  m_Control3;
    ExtCheckedPointer<IDebugControl4>  m_Control4;
    ExtCheckedPointer<IDebugDataSpaces2>  m_Data2;
    ExtCheckedPointer<IDebugDataSpaces3>  m_Data3;
    ExtCheckedPointer<IDebugDataSpaces4>  m_Data4;
    ExtCheckedPointer<IDebugRegisters2>  m_Registers2;
    ExtCheckedPointer<IDebugSymbols2>  m_Symbols2;
    ExtCheckedPointer<IDebugSymbols3>  m_Symbols3;
    ExtCheckedPointer<IDebugSystemObjects2>  m_System2;
    ExtCheckedPointer<IDebugSystemObjects3>  m_System3;
    ExtCheckedPointer<IDebugSystemObjects4>  m_System4;
    ULONG  m_OutputWidth;
    ULONG  m_ActualMachine;
    ULONG  m_Machine;
    ULONG  m_PageSize;
    ULONG  m_PtrSize;
    ULONG  m_NumProcessors;
    ULONG64  m_OffsetMask;
    ULONG  m_DebuggeeClass;
    ULONG  m_DebuggeeQual;
    ULONG  m_DumpFormatFlags;
    bool  m_IsRemote;
    bool  m_OutCallbacksDmlAware;
    ULONG  m_OutMask;
    ULONG  m_CurChar;
    ULONG  m_LeftIndent;
    bool  m_AllowWrap;
    bool  m_TestWrap;
    ULONG  m_TestWrapChars;
    PSTR  m_AppendBuffer;
    ULONG  m_AppendBufferChars;
    PSTR  m_AppendAt;
};
```

## <a name="span-idmembersspanspan-idmembersspanspan-idmembersspanmembers"></a><span id="Members"></span><span id="members"></span><span id="MEMBERS"></span>メンバー


<span id="m_ExtMajorVersion"></span><span id="m_extmajorversion"></span><span id="M_EXTMAJORVERSION"></span>**m\_ExtMajorVersion**  
拡張機能ライブラリのメジャー バージョン番号。 これで設定する必要があります、 [**初期化**](https://msdn.microsoft.com/library/windows/hardware/ff550945)メソッド。 設定されていない場合に既定値**1**します。

<span id="m_ExtMinorVersion"></span><span id="m_extminorversion"></span><span id="M_EXTMINORVERSION"></span>**m\_ExtMinorVersion**  
拡張機能ライブラリのマイナー バージョン番号。 これで設定する必要があります、 [**初期化**](https://msdn.microsoft.com/library/windows/hardware/ff550945)メソッド。 設定されていない場合に既定値**0** (ゼロ)。

<span id="m_ExtInitFlags"></span><span id="m_extinitflags"></span><span id="M_EXTINITFLAGS"></span>**m\_ExtInitFlags**  
DbgEng 拡張機能の初期化フラグ[ *DebugExtensionInitialize*](https://msdn.microsoft.com/library/windows/hardware/ff540476)します。

<span id="m_KnownStructs"></span><span id="m_knownstructs"></span><span id="M_KNOWNSTRUCTS"></span>**m\_KnownStructs**  
配列の[ **ExtKnownStruct** ](https://msdn.microsoft.com/library/windows/hardware/ff543985)拡張ライブラリは、出力の書式設定の対応する構造体。 このメンバーを設定する必要があります、 [**初期化**](https://msdn.microsoft.com/library/windows/hardware/ff550945)メソッドとは、このメソッドから戻ると、変更できません。

場合**m\_KnownStructs**ない**NULL**、 **TypeName** 、最後のメンバー **ExtKnownStruct**配列内の構造必要があります**NULL**します。

構造体の型の名前と一致する場合は、出力では、ターゲットの構造をフォーマットするときに、 **TypeName**のいずれかのメンバー、 **ExtKnownStruct**コールバック関数が指定された、この配列内の構造体**メソッド**書式設定を実行するメンバーが呼び出されます。

<span id="m_ProvidedValues"></span><span id="m_providedvalues"></span><span id="M_PROVIDEDVALUES"></span>**m\_ProvidedValues**  
配列の**ExtProvidedValue**構造擬似を一覧表示拡張機能ライブラリの値を提供できることを登録します。 このメンバーを設定する必要があります、 [**初期化**](https://msdn.microsoft.com/library/windows/hardware/ff550945)メソッドとは、このメソッドから戻ると、変更できません。

場合**m\_ProvidedValues**ない**NULL**、 **ValueName** 、最後のメンバー **ExtProvidedValue**構造体、配列である必要があります**NULL**します。

仮想デバイスの名前の登録と一致する場合に、擬似レジスタを評価するときに、 **ValueName**のいずれかのメンバー、 **ExtProvidedValue** でコールバック関数が指定された、この配列内の構造体**メソッド**擬似レジスタを評価するメンバーが呼び出されます。

<span id="m_Advanced"></span><span id="m_advanced"></span><span id="M_ADVANCED"></span>**m\_高度な**  
[ **IDebugAdvanced** ](https://msdn.microsoft.com/library/windows/hardware/ff549798)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。

<span id="m_Client"></span><span id="m_client"></span><span id="M_CLIENT"></span>**m\_クライアント**  
[ **IDebugClient** ](https://msdn.microsoft.com/library/windows/hardware/ff549827)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。

<span id="m_Control"></span><span id="m_control"></span><span id="M_CONTROL"></span>**m\_コントロール**  
[ **IDebugControl** ](https://msdn.microsoft.com/library/windows/hardware/ff550508)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。

<span id="m_Data"></span><span id="m_data"></span><span id="M_DATA"></span>**m\_データ**  
[ **IDebugDataSpaces** ](https://msdn.microsoft.com/library/windows/hardware/ff550528)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。

<span id="m_Registers"></span><span id="m_registers"></span><span id="M_REGISTERS"></span>**m\_を登録します**  
[ **IDebugRegisters** ](https://msdn.microsoft.com/library/windows/hardware/ff550825)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。

<span id="m_Symbols"></span><span id="m_symbols"></span><span id="M_SYMBOLS"></span>**m\_シンボル**  
[ **IDebugSymbols** ](https://msdn.microsoft.com/library/windows/hardware/ff550856)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。

<span id="m_System"></span><span id="m_system"></span><span id="M_SYSTEM"></span>**m\_システム**  
[ **IDebugSystemObjects** ](https://msdn.microsoft.com/library/windows/hardware/ff550875)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。

<span id="m_Advanced2"></span><span id="m_advanced2"></span><span id="M_ADVANCED2"></span>**m\_Advanced2**  
[ **IDebugAdvanced2** ](https://msdn.microsoft.com/library/windows/hardware/ff549798)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_Advanced3"></span><span id="m_advanced3"></span><span id="M_ADVANCED3"></span>**m\_Advanced3**  
[ **IDebugAdvanced3** ](https://msdn.microsoft.com/library/windows/hardware/ff549798)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_Client2"></span><span id="m_client2"></span><span id="M_CLIENT2"></span>**m\_Client2**  
[ **IDebugClient2** ](https://msdn.microsoft.com/library/windows/hardware/ff549827)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_Client3"></span><span id="m_client3"></span><span id="M_CLIENT3"></span>**m\_Client3**  
[ **IDebugClient3** ](https://msdn.microsoft.com/library/windows/hardware/ff549827)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_Client4"></span><span id="m_client4"></span><span id="M_CLIENT4"></span>**m\_Client4**  
[ **IDebugClient4** ](https://msdn.microsoft.com/library/windows/hardware/ff549827)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_Client5"></span><span id="m_client5"></span><span id="M_CLIENT5"></span>**m\_Client5**  
[ **IDebugClient5** ](https://msdn.microsoft.com/library/windows/hardware/ff549827)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_Control2"></span><span id="m_control2"></span><span id="M_CONTROL2"></span>**m\_Control2**  
[ **IDebugControl2** ](https://msdn.microsoft.com/library/windows/hardware/ff550508)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_Control3"></span><span id="m_control3"></span><span id="M_CONTROL3"></span>**m\_Control3**  
[ **IDebugControl3** ](https://msdn.microsoft.com/library/windows/hardware/ff550508)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_Control4"></span><span id="m_control4"></span><span id="M_CONTROL4"></span>**m\_Control4**  
[ **IDebugControl4** ](https://msdn.microsoft.com/library/windows/hardware/ff550508)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_Data2"></span><span id="m_data2"></span><span id="M_DATA2"></span>**m\_Data2**  
[ **IDebugDataSpaces2** ](https://msdn.microsoft.com/library/windows/hardware/ff550528)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_Data3"></span><span id="m_data3"></span><span id="M_DATA3"></span>**m\_Data3**  
[ **IDebugDataSpaces3** ](https://msdn.microsoft.com/library/windows/hardware/ff550528)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_Data4"></span><span id="m_data4"></span><span id="M_DATA4"></span>**m\_Data4**  
[IDebugDataSpaces4](https://msdn.microsoft.com/library/windows/hardware/ff550528)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_Registers2"></span><span id="m_registers2"></span><span id="M_REGISTERS2"></span>**m\_Registers2**  
[ **IDebugRegisters2** ](https://msdn.microsoft.com/library/windows/hardware/ff550825)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_Symbols2"></span><span id="m_symbols2"></span><span id="M_SYMBOLS2"></span>**m\_Symbols2**  
[ **IDebugSymbols2** ](https://msdn.microsoft.com/library/windows/hardware/ff550856)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_Symbols3"></span><span id="m_symbols3"></span><span id="M_SYMBOLS3"></span>**m\_Symbols3**  
[ **IDebugSymbols3** ](https://msdn.microsoft.com/library/windows/hardware/ff550856)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_System2"></span><span id="m_system2"></span><span id="M_SYSTEM2"></span>**m\_システム 2**  
[ **IDebugSystemObjects2** ](https://msdn.microsoft.com/library/windows/hardware/ff550875)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_System3"></span><span id="m_system3"></span><span id="M_SYSTEM3"></span>**m\_System3**  
[ **IDebugSystemObjects3** ](https://msdn.microsoft.com/library/windows/hardware/ff550875)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_System4"></span><span id="m_system4"></span><span id="M_SYSTEM4"></span>**m\_system4 のマニュアル ページ**  
[ **IDebugSystemObjects4** ](https://msdn.microsoft.com/library/windows/hardware/ff550875)拡張機能ライブラリで使用できるクライアント オブジェクトのインターフェイス ポインター。 拡張の外部から呼び出されるメソッドの呼び出し中に無効です-たとえば、拡張機能の実行コマンドを呼び出し[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)と**ExtProvideValueMethod**します。 このインターフェイスは、デバッガー エンジンのすべてのバージョンでできない可能性があります。

<span id="m_PtrSize"></span><span id="m_ptrsize"></span><span id="M_PTRSIZE"></span>**m\_から検出しました。**  
現在のターゲットのポインターのサイズ。 ターゲットは、32 ビット ポインターを使用している場合**m\_から検出した**は 4 です。 ターゲットは、64 ビットのポインターを使用している場合**m\_から検出した**は 8 です。

<span id="m_AppendBuffer"></span><span id="m_appendbuffer"></span><span id="M_APPENDBUFFER"></span>**m\_AppendBuffer**  
拡張ライブラリからエンジンに文字列を返すために使用する文字のバッファー。 このバッファーのサイズは**m\_AppendBufferChars**します。 メソッド**AppendBufferString**、 **AppendStringVa**、および**もう 1 つ**このバッファーに文字列を書き込むために使用できます。

<span id="m_AppendBufferChars"></span><span id="m_appendbufferchars"></span><span id="M_APPENDBUFFERCHARS"></span>**m\_AppendBufferChars**  
文字バッファーのサイズを**m\_AppendBuffer**します。









