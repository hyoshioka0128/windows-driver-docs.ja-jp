---
title: GDL プリプロセスでの論理演算子での問題
description: GDL プリプロセスでの論理演算子での問題
ms.assetid: 8ba1758c-8b8e-4eb2-8625-ffee213025aa
keywords:
- プリプロセッサ ディレクティブ WDK GDL、前処理に関する問題
- WDK GDL、ソース ファイルのプリプロセッサ ディレクティブのディレクティブ
- ソース ファイル WDK GDL、前処理に関する問題
- プリプロセッサ ディレクティブ WDK GDL、論理演算子
- WDK GDL の論理演算子
- NOT 演算子 WDK GDL
- AND 演算子 WDK GDL
- OR 演算子 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79ce6bb7e1f9fa21eefb1e2461a53c087ce43450
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538108"
---
# <a name="problems-with-logical-operators-in-gdl-preprocessing"></a>GDL プリプロセスでの論理演算子での問題


GDL プリプロセッサ条件の論理演算子は現在サポートされていませんが、シミュレーションを行うことができます。

### <a href="" id="simulating-the-not-operator"></a> NOT 演算子をシミュレートします。

NOT 演算子を使用して、として次のコード例は通常可能性があります。

```cpp
#Ifdef:  symbol
--do this--
#Endif: 
```

ただし、代わりに次のコード例を使用する必要があります。

```cpp
#Ifdef:  symbol
#Else:
--do this--
#Endif: 
```

### <a href="" id="simulating-the-and-operator"></a> AND 演算子をシミュレートします。

AND 演算子を使用して、次のコード例に示すよう通常可能性があります。

```cpp
#Ifdef:  (symbolA  *AND* symbolB)
--do this--
#Endif: 
```

ただし、代わりに次のコード例を使用する必要があります。

```cpp
#Ifdef:  symbolA
#Ifdef:  symbolB
--do this--
#Endif: 
#Endif: 
```

### <a href="" id="simulating-the-or-operator"></a> OR 演算子をシミュレートします。

OR 演算子を使用して、次のコード例に示すよう通常可能性があります。

```cpp
#Ifdef:  (symbolA  *OR* symbolB)
--do this--
#Endif: 
```

ただし、代わりに次のコード例を使用する必要があります。

```cpp
#Ifdef:  symbolA
#Define: TempSymbol
#Elseifdef: symbolB
#Define: TempSymbol
#Endif: 
#Ifdef:  TempSymbol
--do this--
#Endif: 
#Undefine: TempSymbol
```

 

 




