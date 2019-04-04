---
title: ドライバー オブジェクト内のドライバー エントリ ポイント
description: ドライバー オブジェクト内のドライバー エントリ ポイント
ms.assetid: f004c2b3-8435-4c25-82e9-aff3911dc316
keywords:
- ドライバー オブジェクトの WDK カーネル
- 標準のドライバー ルーチン WDK カーネル ドライバー オブジェクト
- ドライバー ルーチン WDK カーネル ドライバー オブジェクト
- ルーチン WDK カーネル ドライバー オブジェクト
- WDK ドライバー オブジェクトのオブジェクト
- エントリ ポイントの WDK カーネル
- ドライバーのエントリ ポイントの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fdf835318841a22e843126d5157fd724ba5fb88
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538117"
---
# <a name="driver-entry-points-in-driver-objects"></a>ドライバー オブジェクト内のドライバー エントリ ポイント





カーネル モード ドライバーでは、そのドライバー オブジェクトで、次のエントリ ポイントを指定する必要があります。

-   少なくとも 1 つのディスパッチ ルーチンの PnP、電源、Irp の要求を取得するために、エントリ ポイントと I/O 操作。

-   エントリ ポイントの[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)で、日常的な**DriverObject -&gt; DriverExtension -&gt; AddDevice**します。

-   エントリ ポイントの[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858) Irp のキューを管理する場合は、ルーチン。

-   ドライバーの読み込みや、動的に置き換えられますことができる場合、 [*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)システム オブジェクトや、ドライバーが割り当てたメモリなどの任意のシステム リソースを解放するために、エントリ ポイント。 (キーボード ドライバーなど、システムの実行中に置き換えることのできないドライバーの指定は、*アンロード*ルーチン)。

これらの要件は、いくつかのミニポート ドライバーを対応するクラスまたはポートのドライバー エントリ ポイントを定義、ドライバー オブジェクトには適用されません。 詳細については、デバイスの種類に固有のドキュメントを参照してください。

I/O マネージャーは、対応するドライバー オブジェクト内のデバイスのドライバーが作成したオブジェクトに関する情報を保持します。

ドライバーが読み込まれるときにその[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ドライバー オブジェクトへのポインターとルーチンが呼び出されます。 ドライバーの場合に**DriverEntry**ルーチンを呼び出すと、設定*ディスパッチ*、 *StartIo* (ある場合)、および*アンロード*(あれば) エントリ ポイント直接ドライバーのオブジェクトには、次のように。

```cpp
DriverObject->MajorFunction[IRP_MJ_xxx] = DDDispatchXxx; 
              :    : 
DriverObject->MajorFunction[IRP_MJ_yyy] = DDDispatchYyy; 
              :    : 
DriverObject->DriverStartIo = DDStartIo; 
DriverObject->DriverUnload = DDUnload; 
              :    : 
```

**DriverEntry**ルーチンのエントリ ポイントを設定もその*AddDevice*で、日常的な**DriverExtension**の次のように、そのドライバー オブジェクト。

```cpp
DriverObject->DriverExtension->AddDevice = DDAddDevice; 
```

A **DriverEntry**または省略可能な[*を再初期化*](https://msdn.microsoft.com/library/windows/hardware/ff561022)ルーチンはまたドライバー オブジェクト内のフィールドを使用できます (に表示されていない、[ドライバー オブジェクトの図は](introduction-to-driver-objects.md#driver-object-illustration))情報を取得したり、configuration manager のレジストリのデータベースに情報を設定します。 詳細については、[ドライバーのレジストリ キー](https://msdn.microsoft.com/library/windows/hardware/ff549538)を参照してください。

I/O マネージャーにはドライバー オブジェクトを操作するサポート ルーチン エクスポートしない[**ドライバー\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff544174)構造体。 ドライバー オブジェクトは、現在読み込まれているドライバーを追跡する I/O マネージャーによって使用されます。 ドライバー オブジェクトの一部のメンバーは、I/O マネージャーでのみ使用されます。 他のユーザーでもメンバーを使用するドライバーのライターです。たとえばを定義するには、特定のメンバー名を認識する必要があります*AddDevice*、*ディスパッチ*、 *StartIo*、および*アンロード*エントリ ポイント。 内のドキュメントに未記載のメンバーを使用する必要がありますとも、**ドライバー\_オブジェクト**構造体も、このドキュメントで名前がドライバー オブジェクトのメンバーの場所に関する前提条件を作成します。 それ以外の場合、1 つの Windows プラットフォームから別のドライバーの移植性を維持することはできません。

 

 




