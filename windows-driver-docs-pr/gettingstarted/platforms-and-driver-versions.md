---
title: 異なるバージョンの Windows に対するドライバーの作成
description: 異なるバージョンの Windows に対するドライバーの作成
ms.assetid: 7519235c-46c5-49aa-8b11-9e9ac5a51026
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b32b135f00ba40f3d8cbf267bff7c19fb3973b50
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363673"
---
# <a name="writing-drivers-for-different-versions-of-windows"></a>異なるバージョンの Windows に対するドライバーの作成


ドライバー プロジェクトを作るときに、最低ターゲット オペレーティング システム、つまりドライバーを実行する Windows の最低限のバージョンを指定します。 たとえば、Windows 7 を最低ターゲット オペレーティング システムとして指定することができます。 その場合、ドライバーは、Windows 7 とそれ以降のバージョンの Windows で実行されることになります。

**注**  ある最低バージョンの Windows に向けてドライバーを開発する場合、そのドライバーを以降のバージョンの Windows で動作させたいときは、文書化されていない関数を使うことはできません。また、文書化されている関数であっても、ドキュメントに記載されていない方法で使うことはできません。 このような使い方をすると、以降のバージョンの Windows でドライバーは動作しなくなる可能性があります。 また、文書化された関数だけを慎重に使っている場合でも、新しいバージョンの Windows がリリースされるごとにそのバージョンでドライバーをテストするようにしてください。



## <a name="span-idwriting_a_multiversion_driver_using_only_common_featuresspanspan-idwriting_a_multiversion_driver_using_only_common_featuresspanspan-idwriting_a_multiversion_driver_using_only_common_featuresspanwriting-a-multiversion-driver-using-only-common-features"></a><span id="Writing_a_multiversion_driver_using_only_common_features"></span><span id="writing_a_multiversion_driver_using_only_common_features"></span><span id="WRITING_A_MULTIVERSION_DRIVER_USING_ONLY_COMMON_FEATURES"></span>共通の機能を使ったマルチバージョン ドライバーの作成


複数のバージョンの Windows で実行するドライバーを設計する場合、最もわかりやすいアプローチは、そのドライバーを実行するあらゆるバージョンの Windows に共通した DDI 関数と構造体以外は、使用を許可しないという方法です。 こうした状況では、このドライバーがサポートする最も早期の Windows バージョンに最低ターゲット オペレーティング システムを設定します。

たとえば、Windows 7 から始まるすべてのバージョンの Windows をサポートする場合は、次のようにします。

1.  ドライバーが Windows 7 で提供されている機能だけを使うようにドライバーを設計、実装します。

2.  ドライバーのビルド時に、最低ターゲット オペレーティング システムとして Windows 7 を指定します。

このプロセスはシンプルである半面、ドライバーには、以降のバージョンの Windows から提供される機能についてはそのサブセットだけを使うという制限が適用されます。

## <a name="span-idwriting_a_multiversion_driver_that_uses_version-dependent_featuresspanspan-idwriting_a_multiversion_driver_that_uses_version-dependent_featuresspanspan-idwriting_a_multiversion_driver_that_uses_version-dependent_featuresspanwriting-a-multiversion-driver-that-uses-version-dependent-features"></a><span id="Writing_a_multiversion_driver_that_uses_version-dependent_features"></span><span id="writing_a_multiversion_driver_that_uses_version-dependent_features"></span><span id="WRITING_A_MULTIVERSION_DRIVER_THAT_USES_VERSION-DEPENDENT_FEATURES"></span>特定バージョンに依存する機能を使ったマルチバージョン ドライバーの作成


カーネル モード ドライバーでは、ドライバーが実行されている Windows のバージョンを動的に特定できるほか、そのバージョンで利用可能な機能を使うことができるようになります。 たとえば、Windows 7 以降のすべての Windows バージョンをサポートする必要のあるドライバーの場合、実行時に現在動作中の Windows バージョンを特定することができます。 ドライバーが Windows 7 で実行されている場合は、必ず Windows 7 がサポートする DDI 関数だけを使います。 ただし、たとえば、ドライバーの実行時チェックにより、Windows 8 で動作中であると判断された場合は、Windows 8 に固有の追加 DDI 関数も同じドライバーで使うことができます。

### <a name="span-iddetermining_the_windows_versionspanspan-iddetermining_the_windows_versionspandetermining-the-windows-version"></a><span id="determining_the_windows_version"></span><span id="DETERMINING_THE_WINDOWS_VERSION"></span>Windows バージョンの特定

[**RtlIsNtDdiVersionAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlisntddiversionavailable) は、Windows の特定バージョンで提供される機能が利用可能かどうかを、ドライバーが実行時に判断するために利用できる関数です。 この関数のプロトタイプは次のとおりです。

```cpp
BOOLEAN RtlIsNtDdiVersionAvailable(IN ULONG Version)
```

このプロトタイプで、*Version* は、必要な Windows DDI バージョンを表す値です。 この値は、sdkddkver.h で定義された DDI バージョン定数のいずれか (NTDDI\_WIN8、NTDDI\_WIN7 など) でなければなりません。

[**RtlIsNtDdiVersionAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlisntddiversionavailable) は、呼び出し元が *Version* で指定されたバージョン、またはそれ以降の Windows で実行されている場合に、TRUE を返します。

ドライバーでは、[**RtlIsServicePackVersionInstalled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlisservicepackversioninstalled) 関数を呼び出すことにより、特定のサービス パックのチェックを実行することもできます。 この関数のプロトタイプは次のとおりです。

```cpp
BOOLEAN RtlIsServicePackVersionInstalled(IN ULONG Version)
```

このプロトタイプで、*Version* は、必要な Windows バージョンとサービス パックを表す値です。 この値は、sdkddkver.h で定義された DDI バージョン定数のいずれか (NTDDI\_WS08SP3 など) でなければなりません。

[  **RtlIsServicePackVersionInstalled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlisservicepackversioninstalled) は、オペレーティング システムのバージョンと、指定されたバージョンが一致した場合に限り、TRUE を返します。 したがって、*Version* を NTDDI\_WS08SP3 に設定して **RtlIsServicePackVersionInstalled** を呼び出すと、ドライバーが Windows Server 2008 SP4 で実行されていない限り、失敗することになります。

### <a name="span-idconditionally_calling_windows_version_dependent_functionsspanspan-idconditionally_calling_windows_version_dependent_functionsspanconditionally-calling-windows-version-dependent-functions"></a><span id="conditionally_calling_windows_version_dependent_functions"></span><span id="CONDITIONALLY_CALLING_WINDOWS_VERSION_DEPENDENT_FUNCTIONS"></span>Windows バージョンに依存する関数の条件付き呼び出し

ドライバーは、コンピューター上で指定したバージョンのオペレーティング システムが利用可能と判断した後、[**MmGetSystemRoutineAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetsystemroutineaddress) 関数を使って、ルーチンを動的に探したり、ポインターを介してこの関数を呼び出すことができます。 この関数は、Windows 7 とそれ以降のオペレーティング システム バージョンで利用可能です。

**注**  型チェックの結果を維持し、意図しないエラーを防ぐために、元の関数の型をミラー化した typedef を作る必要があります。



### <a name="span-idexample__determining_the_windows_version_and_conditionally_calling_a_vspanspan-idexample__determining_the_windows_version_and_conditionally_calling_a_vspanexample-determining-the-windows-version-and-conditionally-calling-a-version-dependent-function"></a><span id="example__determining_the_windows_version_and_conditionally_calling_a_v"></span><span id="EXAMPLE__DETERMINING_THE_WINDOWS_VERSION_AND_CONDITIONALLY_CALLING_A_V"></span>例: Windows バージョンを特定してバージョンに依存する関数を条件付きで呼び出す

次のコード例は、ドライバーのヘッダー ファイルを抜粋したもので、[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)) 関数に対するポインターとして PAISQSL 型を定義しています。 この例では、この関数と同じ型の `AcquireInStackQueuedSpinLock` 変数を宣言しています。

```cpp
...
 //
// Pointer to the ordered spin lock function.
// This function is only available on Windows 7 and
// later systems
 typedef (* PAISQSL) (KeAcquireInStackQueuedSpinLock);
PAISQSL AcquireInStackQueued = NULL;
 ...
```

ドライバーの初期化コードを抜粋した次のコード例では、ドライバーが Windows 7 またはそれ以降のオペレーティング システムで実行されているかどうかを判断します。 Windows 7 またはそれ以降のオペレーティング システムで実行されている場合は、[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)) へのポインターが取得されます。

```cpp
...

//
// Are we running on Windows 7 or later?
//
 if (RtlIsNtDdiVersionAvailable(NTDDI_WIN7) ) {

 //
  // Yes... Windows 7 or later it is!
  //
     RtlInitUnicodeString(&funcName,
                  L"KeAcquireInStackQueuedSpinLock");

 //
  // Get a pointer to Windows implementation
  // of KeAcquireInStackQueuedSpinLock into our
  // variable "AcquireInStackQueued"
     AcquireInStackQueued = (PAISQSL)
                  MmGetSystemRoutineAddress(&funcName);
 }

...
// Acquire a spin lock.

 if( NULL != AcquireInStackQueued) {
  (AcquireInStackQueued)(&SpinLock, &lockHandle);
} else {
    KeAcquireSpinLock(&SpinLock);
}
```

この例では、ドライバーが [**RtlIsNtDdiVersionAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlisntddiversionavailable) を呼び出すことにより、ドライバーが Windows 7 またはそれ以降のバージョンで実行されているかどうかを判断します。 バージョンが Windows 7 以降であれば、[**MmGetSystemRoutineAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetsystemroutineaddress) を呼び出して、[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)) 関数に対するポインターを取得し、このポインターを `AcquireInStackQueued` という変数 (PAISQSL 型として宣言されている) に格納します。

後でドライバーがスピン ロックを取得する必要が生じた場合、[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)) 関数に対するポインターを既に受け取っているかどうかを確認します。 このポインターを既に取得している場合、ドライバーはこのポインターにより、**KeAcquireInStackQueuedSpinLock** を呼び出します。 **KeAcquireInStackQueuedSpinLock** へのポインターが null の場合、ドライバーは [**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock) を使ってスピン ロックを取得します。









