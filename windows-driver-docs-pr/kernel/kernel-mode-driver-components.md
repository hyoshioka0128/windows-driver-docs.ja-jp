---
title: カーネル モード ドライバー コンポーネント
description: カーネル モード ドライバー コンポーネント
ms.assetid: 79be2948-cc74-4f0b-8ffa-1e57f44d7b0c
keywords:
- カーネル モード ドライバー WDK、コンポーネント
- カーネル モード ドライバー WDK、標準のドライバーのルーチン
- 標準のドライバーのルーチンの WDK カーネル
- ドライバーのルーチンの WDK カーネル
- ルーチンの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4658ce73b6ae6d7d6cf68dd56c6e7f35ed0e2456
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559958"
---
# <a name="kernel-mode-driver-components"></a>カーネル モード ドライバー コンポーネント





このセクションでは、カーネル モード ドライバーに含まれている標準的な手順について説明します。 これらのいくつか*標準ドライバー ルーチン*; に必要な他のユーザーは省略可能です。 についても説明*ドライバー オブジェクト*、各ドライバーの標準のルーチンへのポインターを含むことができます。

一部のドライバーは、システムが指定したポート ドライバーまたはドライバーの必要な機能の多くを定義するクラスのドライバーと対話します。 たとえば、主に SCSI ミニポート ドライバーが、SCSI ポート ドライバーと対話します。 このようなドライバーでは、必須およびオプションのドライバーのサポートの詳細については、クラス固有のマニュアルを参照してください。

このセクションの内容:

[標準のドライバーのルーチンの概要](introduction-to-standard-driver-routines.md)

[標準のドライバーの日常的な要件](standard-driver-routine-requirements.md)

[ドライバー オブジェクトの概要](introduction-to-driver-objects.md)

[DriverEntry ルーチンを記述します。](writing-a-driverentry-routine.md)

[再初期化ルーチンを記述します。](writing-a-reinitialize-routine.md)

[AddDevice、ルーチンを記述します。](writing-an-adddevice-routine.md)

[書き込みディスパッチ ルーチン](writing-dispatch-routines.md)

[アンロードするルーチンを記述します。](writing-an-unload-routine.md)

 

 




