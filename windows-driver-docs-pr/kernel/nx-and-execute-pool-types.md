---
title: NX と実行プールの種類
description: 非ページプールから割り当てられたメモリを実行不可 (NX) にする必要があるかどうかを示すには、Windows 8 以降の2つの新しいプールの種類を使用できます。
ms.assetid: 954AC53F-270D-4149-AE5D-6BEA7EFAA761
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9d79d7e676f2c595d34a11a004091f181a7d9f7c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838535"
---
# <a name="nx-and-execute-pool-types"></a>NX と実行プールの種類


非ページプールから割り当てられたメモリを実行不可 (NX) にする必要があるかどうかを示すには、Windows 8 以降の2つの新しいプールの種類を使用できます。 これらのプールの種類は、次のプールの種類によって[ **\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_pool_type)列挙値として指定されます。

<a href="" id="nonpagedpoolnx"></a>**NonPagedPoolNx**  
NX 非ページプール。 命令は、このプールから割り当てられたメモリ内では実行できません。

<a href="" id="nonpagedpoolexecute"></a>**NonPagedPoolExecute**  
実行可能な非ページプールです。 命令の実行は、このプールから割り当てられたメモリで有効になっています。

ほとんどのドライバーは、割り当てられたメモリのみを使用してデータを格納し、このメモリ内の命令を実行しません。 Windows 8 以降のバージョンの Windows で動作するようにドライバーをビルドする場合は、可能な限り、NX の非ページプールから**NonPagedPoolNx**のメモリを割り当てます。 非ページメモリから命令を実行する必要があるドライバーだけが、実行可能な非ページプールから**NonPagedPoolExecute**メモリを割り当てる必要があります。

Windows 7 以前のバージョンの Windows 用に構築された既存のドライバーについては、 **NonPagedPool**プールの種類を使用すると、ドライバーによって実行可能ファイルプールからメモリが割り当てられます。 **NonPagedPool**定数名には、Windows 8 以降で定義されている**NonPagedPoolExecute**定数名と同じ値が設定されています。 そのため、これらの定数は同じプールの種類を参照します。

Windows 7 またはそれより前のバージョンの windows 用に作成されたドライバーを windows 8 以降のバージョンの windows 用にビルドする場合は、 **NonPagedPool**プールの種類のインスタンスを**NonPagedPoolNx**または**NonPagedPoolExecute**のいずれかで置き換える必要があります。 ドライバー開発者は、この置換を明示的に実行することも、Windows 8 へのドライバーの移植を支援するために用意されているいずれかのオプトイン機構を使用して暗黙的に置き換えることもできます。 詳細については、「 [NX プールのオプトインメカニズム](nx-pool-opt-in-mechanisms.md)」を参照してください。

 

 




