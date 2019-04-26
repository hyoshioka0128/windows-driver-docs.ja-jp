---
title: ファイル ポインターの処理
description: ファイル ポインターの処理
ms.assetid: 9bc03ae0-3e03-492a-b8d7-760eeb18106a
keywords:
- SymProxy、ファイル ポインター
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5830add47c784b98fb535c2c25db92e367856ebe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342028"
---
# <a name="handling-file-pointers"></a>ファイル ポインターの処理


UNC シンボル ストアでは、別の場所にファイル ポインターを使用して、ファイルの場所を検索するクライアント コードを提供する実際のファイルを配置することをサポートします。 SymStore でを使用して、シンボル ストアでこれらのポインターが生成される、 **/p**オプション。 この処理は、他の HTTP ベースのシンボル ストア ファイル ポインターは直接アクセスする UNC の場所を指す場合にのみクライアントでサポートされる、します。 SymProxy が Web サーバーに読み込まれると、ファイル ポインターの処理が自動的に強化されています。 クライアントは、不要になった、HTTP インターフェイスを介して SymProxy が機能しているために、ターゲット ファイルを直接アクセスできる必要があります。

この機能は自動的に適用されるため、場合に、一部のファイルと他のユーザーの通常のファイル ポインターの実装を提供するために、プロキシを使用する必要がありますを無効にするオプションがあります。 これを行うには、作成、REG\_DWORD で"NoFilePointerHandler"をという**HKLM\\ソフトウェア\\Microsoft\\シンボル サーバー**します。 SymProxy で内部ファイル ポインターのハンドラーを無効にする 1 (または 0 以外) には、この値を設定します。

 

 





