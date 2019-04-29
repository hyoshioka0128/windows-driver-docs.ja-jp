---
title: ファイル システム スタック
description: ファイル システム スタック
ms.assetid: 67839ffb-fe38-42c2-8f33-89d01d796d8a
keywords:
- フィルター ドライバー WDK ファイル システム、ファイル システム スタック
- ファイル システム フィルター ドライバー WDK、ファイル システム スタック
- ファイル システム スタック WDK
- WDK のボリュームのファイル システム、デバイス オブジェクト
- VDOs WDK ファイル システム
- デバイス オブジェクトの WDK ファイル システムを制御します。
- CDOs WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4bb14882df90f38400cb7291fd83a03a9e0de59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383825"
---
# <a name="file-system-stacks"></a>ファイル システム スタック


## <span id="ddk_file_system_stacks_if"></span><span id="DDK_FILE_SYSTEM_STACKS_IF"></span>


ファイル システム ドライバーは、2 つの異なる種類のデバイス オブジェクトを作成します。 デバイス オブジェクト (CDO) とボリュームのデバイス オブジェクト (提供) を制御します。 A*ファイル システム スタック*にアタッチされているファイル システム フィルター ドライバーのフィルター デバイス オブジェクトと共に、これらのデバイス オブジェクトのいずれかで構成します。 ファイル システムのデバイス オブジェクトは、常に、スタックの一番下を形成します。

### <a name="span-idddkfilesystemcontroldeviceobjectsifspanspan-idddkfilesystemcontroldeviceobjectsifspanfile-system-control-device-objects"></a><span id="ddk_file_system_control_device_objects_if"></span><span id="DDK_FILE_SYSTEM_CONTROL_DEVICE_OBJECTS_IF"></span>ファイル システム コントロールのデバイス オブジェクト

ファイル システム コントロールのデバイス オブジェクトでは、個々 のボリュームではなくファイル全体のシステムを表すし、グローバルなファイル システムのキューに格納されます。 ファイル システムを作成またはでデバイス オブジェクトがコントロールの詳細は名前付きの**DriverEntry**ルーチン。 たとえば、FastFat が 2 つの CDOs を作成します: 1 つは固定メディア、リムーバブル メディアのいずれか。 CDF は、リムーバブル メディアのみがあるため、1 つだけの CDO を作成します。

ファイル システム コントロールのデバイス オブジェクトは、名前を指定するために必要です。 これは、多くのカーネル モードとファイル システム フィルター ドライバー、ルーチンをサポートするため、このボリュームのデバイス オブジェクトと離れていることを示す方法としてデバイス オブジェクトをコントロールの違いに依存します。

### <a name="span-idddkfilesystemvolumedeviceobjectsifspanspan-idddkfilesystemvolumedeviceobjectsifspanfile-system-volume-device-objects"></a><span id="ddk_file_system_volume_device_objects_if"></span><span id="DDK_FILE_SYSTEM_VOLUME_DEVICE_OBJECTS_IF"></span>ファイル システム ボリュームのデバイス オブジェクト

ファイル システム ボリュームのデバイス オブジェクトは、ファイル システムでマウントされたボリュームを表します。 ファイル システムは、ボリュームのマウント要求に対する応答では、通常のボリュームをマウントするときに、ボリューム デバイス オブジェクトを作成します。 制御デバイス オブジェクトとは異なり、ボリューム デバイス オブジェクトは、特定の論理的または物理的な記憶域デバイスに関連付けられては常にします。

**注**  コントロール デバイス オブジェクトとは異なりボリューム デバイス オブジェクトする必要がありますしないために名前を指定、ボリューム デバイス オブジェクトの名前を付け、セキュリティ ホールを作成します。

 

 

 




