---
title: プールの種類 (NX と Execute)
description: 示すかどうか非ページ プールから割り当てられたメモリはいいえ-実行される (NX) には、するには、Windows 8 以降では、2 つの新しいプール型を使用できます。
ms.assetid: 954AC53F-270D-4149-AE5D-6BEA7EFAA761
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1a0841f6e3bf648b81ce27e24dd953830badeb1c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365422"
---
# <a name="nx-and-execute-pool-types"></a>プールの種類 (NX と Execute)


示すかどうか非ページ プールから割り当てられたメモリはいいえ-実行される (NX) には、するには、Windows 8 以降では、2 つの新しいプール型を使用できます。 これらのプールの種類は、次によって指定された[**プール\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_pool_type)列挙値。

<a href="" id="nonpagedpoolnx"></a>**NonPagedPoolNx**  
NX 非ページ プール。 手順については、このプールから割り当てられたメモリで実行できません。

<a href="" id="nonpagedpoolexecute"></a>**NonPagedPoolExecute**  
実行可能ファイルの非ページ プール。 命令の実行は、このプールから割り当てられたメモリで有効です。

ほとんどのドライバーでは、割り当てられたメモリを使用して、データの保存にしか、このメモリ内の手順を実行しないでください。 Windows 8 および Windows の以降のバージョンで実行するには、ドライバーをビルドする場合は、割り当てる**NonPagedPoolNx**メモリ、NX から可能な限り、非ページ プール。 非ページ メモリから命令を実行する必要があるドライバーのみを割り当てる必要があります**NonPagedPoolExecute**実行可能ファイルの非ページ プールからメモリ。

既存のドライバーを使用する場合は、Windows 7 と以前のバージョンの Windows では、組み込まれているため、 **NonPagedPool**プールの種類には、ドライバーは、実行可能なプールからメモリを割り当てます。 **NonPagedPool**定数名と同じ値を持つ、 **NonPagedPoolExecute** Windows 8 以降では定義されている定数の名前。 そのため、これらの定数は、同じプールの種類を参照してください。

Windows 8 または Windows でのインスタンスの以降のバージョンの Windows 7 または Windows の以前のバージョン用に記述されたドライバーが構築されたかどうか、 **NonPagedPool**プールの種類は、いずれかで置き換える必要があります**NonPagedPoolNx**または**NonPagedPoolExecute**します。 ドライバーの開発者は、この交換を明示的に実行することができますか、またはそのドライバーを Windows 8 に移植することに開発者を支援するために提供されるオプトイン メカニズムのいずれかを使用して、置換を暗黙的に実行できます。 詳細については、次を参照してください。[プール オプトイン メカニズムに NX](nx-pool-opt-in-mechanisms.md)します。

 

 




