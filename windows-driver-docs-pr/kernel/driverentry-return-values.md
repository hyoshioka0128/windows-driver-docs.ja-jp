---
title: DriverEntry の戻り値
description: DriverEntry の戻り値
ms.assetid: 052be2ea-375a-4495-931e-8b66972125a5
keywords:
- DriverEntry WDK カーネルでは、戻り値
- WDK DriverEntry ルーチンの戻り値
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb670ddabd19032ab68d5d5ce1d0939632e53264
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359470"
---
# <a name="driverentry-return-values"></a>DriverEntry の戻り値





A [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンを返します、 [NTSTATUS 値](ntstatus-values.md)、いずれかの状態\_成功またはエラーを適切な状態です。

**DriverEntry**ルーチンへの呼び出しを延期する[ **IoRegisterDriverReinitialization** ](https://msdn.microsoft.com/library/windows/hardware/ff549511)の直前にステータスを返すまで\_成功します。 状態が返されます場合を除き、この呼び出しを行う必要がありますいない、\_成功します。

場合、 **DriverEntry**ルーチンは成功ではない NTSTATUS 値または状態などの情報の値を返します\_成功すると、そのドライバー **DriverEntry**ルーチンが読み込まれていません。

A **DriverEntry**任意のシステム オブジェクト、システム リソース、およびレジストリのリソースが既に設定されているコントロールを返す前に初期化が失敗するルーチンを解放する必要があります。 ドライバーのディスパッチのエントリ ポイントのドライバー オブジェクトをリセットする必要があります[ **IRP\_MJ\_フラッシュ\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff550760)と[ **IRP\_MJ\_シャット ダウン**](https://msdn.microsoft.com/library/windows/hardware/ff550807)に**NULL**ドライバーは、これらの要求をサポートしている場合。

ドライバーは、初期化に失敗した場合、 **DriverEntry**ルーチンには制御を返す前に、エラーを記録する必要がありますもできます。 します。 参照してください[エラーのログ記録](logging-errors.md)します。

なお、ドライバーの[*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチンは、ドライバーの場合は呼び出されません[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンがエラー状態を返します。

 

 




