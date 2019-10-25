---
title: ライブラリとヘッダー
description: ライブラリとヘッダー
ms.assetid: 0d4d0273-775f-4cbb-8b7f-63b22f3ccdae
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b3b3d89749b120cf33e5a3f8c0c84821f517c874
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827903"
---
# <a name="libraries-and-headers"></a>ライブラリとヘッダー


カーネルモードドライバーは、Ntoskrnl.exe ダイナミックリンクライブラリ (DLL) の**Nt**および**Zw**エントリポイントを呼び出すことによって、ネイティブシステムサービスルーチンを使用します。 この DLL には、これらのルーチンの実際の実装が含まれています。 これらのエントリポイントにアクセスするために、ドライバーは、Windows Driver Kit (WDK) で使用できる Ntoskrnl.exe ライブラリに静的にリンクされています。 Ntoskrnl.exe で実装されるルーチンは、実行時に Ntoskrnl.exe のエントリポイントに動的にリンクするスタブです。

WDK のドキュメントでは、 **Zw**のエントリポイントの一部 (すべてではありません) について説明しています。 ドライバーから呼び出すことができる**Zw**ルーチンの説明については、「 [Zwxxx ルーチン](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff567122(v=vs.85))」を参照してください。

ドキュメント化された**Zw**ルーチンのほとんどは、WDK の Wdm ヘッダーファイルで定義されていますが、いくつかは、Ntddk や Ntifs などの他のヘッダーファイルで定義されています。

通常、ユーザーモードアプリケーションでは、 **Nt**および**Zw**ルーチンは呼び出されません。 代わりに、アプリケーションは、 [CreateFile](https://go.microsoft.com/fwlink/p/?linkid=152795)などの Win32 ルーチンを呼び出すことができます。これにより、要求された操作を実行するために、 [Ntcreatefile](https://go.microsoft.com/fwlink/p/?linkid=157250)や[**zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)などのネイティブシステムサービスルーチンが呼び出されます。 ただし、ユーザーモードアプリケーションでは、Win32 ルーチンでサポートされていない操作を実行するために、 **Nt**または**Zw**ルーチンを直接呼び出す場合があります。

ユーザーモードアプリケーションでは、Ntdll ダイナミックリンクライブラリ内のエントリポイントを呼び出すことによって、ネイティブシステムサービスルーチンを使用します。 これらのエントリポイントは、 **Nt**および**Zw**ルーチンへの呼び出しを、カーネルモードにトラップされるシステム呼び出しに変換します。 これらのエントリポイントにアクセスするために、ユーザーモードアプリケーションは、WDK で使用できる Ntdll ライブラリに静的にリンクします。 Ntdll で実装されるルーチンは、実行時に Ntdll のエントリポイントに動的にリンクするスタブです。

Windows SDK のドキュメントでは、Ntdll の**Nt**エントリポイントの一部ではありませんが説明されています。 ドキュメントに記載されているほとんどの**Nt**ルーチンは、Windows SDK の Winternl ヘッダーファイルで定義されています。 このドキュメントでは、Zw エントリポイントについて簡単に説明していません。また Windows SDK、のヘッダーファイルに**Zw**ルーチンの定義が含まれていません。

いくつかの小さな例外を除き、 **Nt**ルーチンの Ntdll の各エントリポイントには、 **Zw**ルーチンのエントリポイントが一致しています。 WDK および Windows SDK のドキュメントでは、アプリケーション開発者がドキュメントに記載されていない**Nt**エントリポイントを呼び出さないようにすることを推奨しています。また、今後のバージョンの Windows では、 **Zw**エントリポイントが Ntdll から消失する可能性があることを警告します。 ユーザーモードから**Zw**ルーチンを呼び出すアプリケーション開発者は、このような場合に備えて準備する必要があります。

アプリケーションから呼び出すことができる**Nt**ルーチンの説明については、「 [Winternl](https://go.microsoft.com/fwlink/p/?linkid=157253)、 [Files](https://go.microsoft.com/fwlink/p/?linkid=157254)、および[その他の低レベルクライアントサポート](https://go.microsoft.com/fwlink/p/?linkid=157255)」を参照してください。 Windows SDK のドキュメントに記載されている**Nt**ルーチンの一部の参照ページでは、ルーチンが "非推奨" としてラベル付けされ、推奨されていない**Nt**ルーチンの代わりに同等の Win32 ルーチンを使用するように指示されます。

ユーザーモードのアプリケーションは、Ntoskrnl.exe 内のエントリポイントを呼び出すことができません。また、カーネルモードドライバーは、Ntdll のエントリポイントを呼び出すことができません。

 

 




