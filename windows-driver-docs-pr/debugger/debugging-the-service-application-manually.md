---
title: 手動でサービス アプリケーションのデバッグ
description: 手動でサービス アプリケーションのデバッグ
ms.assetid: 9be3976f-dd56-42f2-ac85-1c5a1f87a4ee
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b6b7f99f96c5e4ed5067ccfb1555b2636dd5329
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549227"
---
# <a name="debugging-the-service-application-manually"></a>手動でサービス アプリケーションのデバッグ


手動でサービス アプリケーションにアタッチが開始された後は、デバッグ、実行中のユーザー モード プロセスと似ています。

使用[TList ツール](tlist.md)で、 **/s**プロセス ID (PID) の各実行中のプロセスとプロセスごとにアクティブなサービスを表示するオプション。

デバッグするサービス アプリケーションが 1 つのプロセスでは、他のサービスと組み合わされている場合は、デバッグする前に分離する必要があります。 これを行うには、サービスの分離で説明する手順を実行します。 この手順の最後に、サービスを再起動します。

サービスの新しい PID を特定するには、次のサービス構成ツール (Sc.exe) コマンドを発行場所*ServiceName*サービスの名前を指定します。

```console
sc queryex ServiceName 
```

これで、ターゲットとしては、このサービス アプリケーションに WinDbg または CDB を起動します。 これを行う 3 つの方法:-pn オプション (実行可能ファイル名が一意である場合、実行可能ファイル名を指定することで、または - psn オプションを使用して、サービス名を指定して-p オプションでは、PID を指定することで。

たとえば、プロセス SpoolSv.exe 651 の PID を持ちという名前のサービスを含む*スプーラー*、次の 3 つのコマンドは同等です。

```console
windbg -p 651 [AdditionalOptions] 
windbg -pn spoolsv.exe [AdditionalOptions] 
windbg -psn spooler [AdditionalOptions] 
```

デバッガーが起動した後は、他のユーザー モード デバッグ セッションで行うように進みます。

 

 





