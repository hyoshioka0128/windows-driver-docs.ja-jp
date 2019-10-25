---
title: ExtExtension
description: ExtExtension クラスは、EngExtCpp extension ライブラリを表すC++クラスの基本クラスです。
ms.assetid: 9c6c4633-df49-4f49-8116-d680bb20c3f5
keywords:
- ExtExtension Windows デバッグ
topic_type:
- apiref
api_name:
- ExtExtension
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f25d147f26847895d94e02d009b69acc36e255a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826423"
---
# <a name="extextension"></a>ExtExtension


**Extextension**クラスは、EngExtCpp extension ライブラリを表すC++クラスの基本クラスです。

**Extextension**クラスには、サブクラスで使用できる次のメソッドが含まれています。

[**化**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))

[**解除**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff558961(v=vs.85))

[**OnSessionActive**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552312(v=vs.85))

[**OnSessionInactive**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552318(v=vs.85))

[**OnSessionAccessible 可能**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552310(v=vs.85))

[**OnSessionInaccessible 不可**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552315(v=vs.85))

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

[**GetNumUnnamedArgs**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548001(v=vs.85))

[**GetUnnamedArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549464(v=vs.85))

[**GetUnnamedArgU64**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549465(v=vs.85))

[**HasUnnamedArg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549733(v=vs.85))

[**GetArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff545586(v=vs.85))

[**GetArgU64**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff545596(v=vs.85))

[**HasArg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549721(v=vs.85))

[**HasCharArg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549727(v=vs.85))

[**SetUnnamedArg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556876(v=vs.85))

[**SetUnnamedArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556878(v=vs.85))

[**SetUnnamedArgU64**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556879(v=vs.85))

[**SetArg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556614(v=vs.85))

[**SetArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556618(v=vs.85))

[**SetArgU64**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556622(v=vs.85))

[**GetRawArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548226(v=vs.85))

**GetRawArgCopy**

**入出力**

**呼びかけ**

**警戒**

**助動詞**

**Dml**

**DmlWarn**

**DmlErr**

**DmlVerb**

**DmlCmdLink**

**DmlCmdExec**

**Refreshoutputのフラグ**

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

**Extextension**クラスには、サブクラスで使用できる次のフィールドも含まれています。

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

## <a name="span-idmembersspanspan-idmembersspanspan-idmembersspanmembers"></a><span id="Members"></span><span id="members"></span><span id="MEMBERS"></span>属する


<span id="m_ExtMajorVersion"></span><span id="m_extmajorversion"></span><span id="M_EXTMAJORVERSION"></span>**m\_ExtMajorVersion**  
拡張ライブラリのメジャーバージョン番号。 これは、 [**Initialize**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))メソッドによって設定する必要があります。 設定されていない場合、既定値は**1**です。

<span id="m_ExtMinorVersion"></span><span id="m_extminorversion"></span><span id="M_EXTMINORVERSION"></span>**m\_ExtMinorVersion**  
拡張ライブラリのマイナーバージョン番号。 これは、 [**Initialize**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))メソッドによって設定する必要があります。 設定されていない場合、既定値は**0** (ゼロ) です。

<span id="m_ExtInitFlags"></span><span id="m_extinitflags"></span><span id="M_EXTINITFLAGS"></span>**m\_ExtInitFlags**  
[*Debugextensioninitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nc-dbgeng-pdebug_extension_initialize)の DbgEng 拡張初期化フラグ。

<span id="m_KnownStructs"></span><span id="m_knownstructs"></span><span id="M_KNOWNSTRUCTS"></span>**m\_KnownStructs**  
拡張ライブラリが出力の書式を設定できる[**Extknownstruct**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/ns-engextcpp-extknownstruct)構造体の配列。 このメンバーは[**Initialize**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))メソッドによって設定される必要があります。このメソッドが返されると、このメンバーを変更することはできません。

**M\_knownstructs**が**null**でない場合、配列内の最後の**Extknownstruct**構造体の**TypeName**メンバーは**null**である必要があります。

出力用のターゲットの構造を書式設定するときに、構造体の型の名前がこの配列内の**Extknownstruct**構造体のいずれかの**TypeName**メンバーと一致する場合、**メソッド**メンバーで指定されたコールバック関数が呼び出されます。書式設定を実行します。

<span id="m_ProvidedValues"></span><span id="m_providedvalues"></span><span id="M_PROVIDEDVALUES"></span>**m\_プロビジョニング値**  
拡張ライブラリが値を提供できる擬似レジスタを一覧表示する**ext/Dedvalue**構造体の配列。 このメンバーは[**Initialize**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))メソッドによって設定される必要があります。このメソッドが返されると、このメンバーを変更することはできません。

**M\_の値**が**null**でない場合は、配列内の最後の**extの Dedvalue**構造体の**ValueName**メンバーが**null**である必要があります。

擬似レジスタを評価するときに、擬似レジスタの名前がこの配列内のいずれかの**Extの値**構造体の**ValueName**メンバーと一致する場合、**メソッド**メンバーで指定されたコールバック関数が呼び出され、擬似レジスタ。

<span id="m_Advanced"></span><span id="m_advanced"></span><span id="M_ADVANCED"></span>**m\_詳細設定**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugAdvanced**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugadvanced)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。

<span id="m_Client"></span><span id="m_client"></span><span id="M_CLIENT"></span>**m\_クライアント**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugclient)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。

<span id="m_Control"></span><span id="m_control"></span><span id="M_CONTROL"></span>**m\_コントロール**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugcontrol)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。

<span id="m_Data"></span><span id="m_data"></span><span id="M_DATA"></span>**m\_データ**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugDataSpaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugdataspaces)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。

<span id="m_Registers"></span><span id="m_registers"></span><span id="M_REGISTERS"></span>**m\_レジスタ**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugregisters)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。

<span id="m_Symbols"></span><span id="m_symbols"></span><span id="M_SYMBOLS"></span>**m\_記号**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugSymbols**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsymbols)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。

<span id="m_System"></span><span id="m_system"></span><span id="M_SYSTEM"></span>**m\_システム**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugSystemObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsystemobjects)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。

<span id="m_Advanced2"></span><span id="m_advanced2"></span><span id="M_ADVANCED2"></span>**m\_Advanced2**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugAdvanced2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugadvanced)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_Advanced3"></span><span id="m_advanced3"></span><span id="M_ADVANCED3"></span>**m\_Advanced3**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugAdvanced3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugadvanced)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_Client2"></span><span id="m_client2"></span><span id="M_CLIENT2"></span>**m\_**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugClient2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugclient)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_Client3"></span><span id="m_client3"></span><span id="M_CLIENT3"></span>**m\_Client3**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugClient3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugclient)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_Client4"></span><span id="m_client4"></span><span id="M_CLIENT4"></span>**m\_Client4**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugClient4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugclient)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_Client5"></span><span id="m_client5"></span><span id="M_CLIENT5"></span>**m\_Client5**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugClient5**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugclient)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_Control2"></span><span id="m_control2"></span><span id="M_CONTROL2"></span>**m\_Control2**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugControl2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugcontrol)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_Control3"></span><span id="m_control3"></span><span id="M_CONTROL3"></span>**m\_Control3**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugControl3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugcontrol)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_Control4"></span><span id="m_control4"></span><span id="M_CONTROL4"></span>**m\_Control4**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugControl4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugcontrol)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_Data2"></span><span id="m_data2"></span><span id="M_DATA2"></span>**m\_Data2**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugDataSpaces2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugdataspaces)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_Data3"></span><span id="m_data3"></span><span id="M_DATA3"></span>**m\_Data3**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugDataSpaces3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugdataspaces)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_Data4"></span><span id="m_data4"></span><span id="M_DATA4"></span>**m\_Data4**  
拡張ライブラリで使用できるクライアントオブジェクトの[IDebugDataSpaces4](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugdataspaces)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_Registers2"></span><span id="m_registers2"></span><span id="M_REGISTERS2"></span>**m\_Registers2**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugRegisters2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugregisters)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_Symbols2"></span><span id="m_symbols2"></span><span id="M_SYMBOLS2"></span>**m\_Symbols2**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugSymbols2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsymbols)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_Symbols3"></span><span id="m_symbols3"></span><span id="M_SYMBOLS3"></span>**m\_Symbols3**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugSymbols3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsymbols)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_System2"></span><span id="m_system2"></span><span id="M_SYSTEM2"></span>**m\_System2**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugSystemObjects2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsystemobjects)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_System3"></span><span id="m_system3"></span><span id="M_SYSTEM3"></span>**m\_System3**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugSystemObjects3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsystemobjects)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_System4"></span><span id="m_system4"></span><span id="M_SYSTEM4"></span>**m\_System4**  
拡張ライブラリで使用できるクライアントオブジェクトの[**IDebugSystemObjects4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsystemobjects)インターフェイスポインター。 これは、外部から呼び出される拡張メソッドの呼び出し中に有効です。たとえば、拡張コマンドの実行、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))と**ExtProvideValueMethod**の呼び出しなどです。 このインターフェイスは、すべてのバージョンのデバッガーエンジンで使用できるとは限りません。

<span id="m_PtrSize"></span><span id="m_ptrsize"></span><span id="M_PTRSIZE"></span>**m\_PtrSize**  
現在のターゲット上のポインターのサイズ。 ターゲットが32ビットポインターを使用している場合、 **m\_PtrSize**は4になります。 ターゲットが64ビットポインターを使用している場合、 **m\_PtrSize**は8です。

<span id="m_AppendBuffer"></span><span id="m_appendbuffer"></span><span id="M_APPENDBUFFER"></span>**m\_AppendBuffer**  
拡張ライブラリからエンジンに文字列を返すために使用される文字バッファー。 このバッファーのサイズは**m\_AppendBufferChars**です。 メソッド**Appendbufferstring**、 **Appendbufferstring**、および**appendstring**を使用して、このバッファーに文字列を書き込むことができます。

<span id="m_AppendBufferChars"></span><span id="m_appendbufferchars"></span><span id="M_APPENDBUFFERCHARS"></span>**m\_AppendBufferChars**  
バッファー **m\_AppendBuffer**のサイズ (文字数)。









