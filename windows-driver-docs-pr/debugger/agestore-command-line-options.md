---
title: AgeStore のコマンドライン オプション
description: AgeStore コマンドラインは、次の構文を使用します。 パラメーターは、任意の順序で含めることができます。
ms.assetid: ae6ad504-a582-45ac-89a1-7e90952948b4
keywords:
- AgeStore コマンド ライン オプションの Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- AgeStore Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 00e28de127720c66f1c0fbd32ce3822069818eb2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327361"
---
# <a name="agestore-command-line-options"></a>AgeStore のコマンドライン オプション


AgeStore コマンドラインは、次の構文を使用します。 パラメーターは、任意の順序で含めることができます。

```console
agestore [PathSpec] -date=Month-Day-Year Options 

agestore [PathSpec] -days=NumberOfDays Options 

agestore [PathSpec] -size=SizeRemaining Options 

agestore [PathSpec] -size Options 

agestore -? 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______PathSpec______"></span><span id="_______pathspec______"></span><span id="_______PATHSPEC______"></span> *PathSpec*   
ファイルが削除対象のターゲット ディレクトリを指定します。 -S オプションを使用すると場合、 *PathSpec*ファイルが削除されるのターゲット ツリーのルート ディレクトリを指定します。 *PathSpec*ローカル コンピューター上のディレクトリの絶対または相対パスまたは UNC パスがあります。 場合*PathSpec*スペースが含まれることは、引用符で囲む必要があります。 場合*PathSpec*は AgeStore 省略すると、現在の作業ディレクトリを使用します。

<span id="-date_Month-Day-Year"></span><span id="-date_month-day-year"></span><span id="-DATE_MONTH-DAY-YEAR"></span>**-日付 =**<em>月-日-年</em>  
ファイルを削除するための終了日を指定します。 指定した日付より前に最後にアクセスされたすべてのファイルは削除されます。 月-日-年、月と日間と、1 日と年の間のハイフンの形式で日付を指定する必要があります。 先頭の 0*月*と*日*は省略可能です。 2 桁または 4 年を指定できます。 2008 年 1 月 5 日の日付を指定するため 01-05-2008 または 1-5-08 として。

<span id="_______-days_NumberOfDays______"></span><span id="_______-days_numberofdays______"></span><span id="_______-DAYS_NUMBEROFDAYS______"></span> **-日 =**<em>NumberOfDays</em>   
ファイルを削除する終了日時を指定します。 指定した数日前の前に最後にアクセスされたすべてのファイルは削除されます。 *NumberOfDays* 24 日数を表す整数を指定します。 たとえば場合、指定子の日 = 3 が 2008 年 2 月 17 日の午後 6時 00分に使用される、2008 年 2 月 14 日の午後 6時 00分より前に最後にアクセスするすべてのファイルが削除されます。

<span id="_______-size_SizeRemaining______"></span><span id="_______-size_sizeremaining______"></span><span id="_______-SIZE_SIZEREMAINING______"></span> **-size=**<em>SizeRemaining</em>   
必要があります (バイト単位)、削除された後に残っているファイルの合計サイズを指定します。 このスイッチを使用すると、AgeStore がターゲット ディレクトリまたはターゲット ツリー内のファイルを削除、ファイルの先頭までは、アクセス最も最近では、残りのファイルの合計サイズが小さいと、以下*SizeRemaining*します。 ときに、 **-s**オプションを使用すると、AgeStore、全体のディレクトリ ツリーを対象とし、 *SizeRemaining*削除後にこのディレクトリ ツリー全体で必要のあるファイルの合計サイズを指定します。

<span id="_______-size______"></span><span id="_______-SIZE______"></span> **-size**   
ターゲット ディレクトリまたはターゲット ツリー内のすべてのファイルの合計サイズを一覧表示する AgeStore をによりします。 ファイルは削除されません。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションの任意の組み合わせ。

<span id="-l"></span><span id="-L"></span>**-l**  
AgeStore せずにこのコマンドが実行された場合に削除されるすべてのファイルを表示するためだけが、すべてのファイルを削除しないことにより、 **-l**オプション。

<span id="-s"></span><span id="-S"></span>**-s**  
下位にディレクトリ全体のツリーを扱う AgeStore *PathSpec*ターゲットとして。 ときに、 **-s**オプションを使用しないで指定されたディレクトリ*PathSpec*ファイルを削除するターゲット ディレクトリになります。 ときに、 **-s**オプションを使用するで指定されたディレクトリ*PathSpec*その下にあるすべてのサブディレクトリになり、ターゲット ツリーにファイルが削除されます。

<span id="-k"></span><span id="-K"></span>**-k**  
空のサブディレクトリを保持する AgeStore をによりします。 このオプションを使用しない場合、AgeStore は、コマンドの実行後が完全に空の場合、ターゲット ディレクトリを削除します。 場合、 **-s**オプションを使用せず、 **-k**オプション、ターゲット ディレクトリ ツリー内のすべての空のディレクトリと削除されます AgeStore にそのファイルの削除 - 自体には、ルート ディレクトリでもが完了した後、空になります。 空にする既に AgeStore 実行する前に発生するこのツリー内のディレクトリがある場合は、AgeStore をこれらのディレクトリも削除します。 ただし、AgeStore コマンドがないファイルの削除により表示された場合 (場合など、 **-サイズ =**<em>SizeRemaining</em>パラメーターは、ターゲット ツリー内のすべてのファイルの合計サイズより大きいサイズを指定します)、空ディレクトリは削除されません。 場合、 **-s**オプションが使用されない空のディレクトリが削除されないと場合、および **-k**オプションは無視されます。

<span id="-q"></span><span id="-Q"></span>**-q**  
Quiet モードです。 このオプションが含まれない場合 AgeStore は、削除されるように、すべてのファイルが一覧表示されます。

<span id="-y"></span><span id="-Y"></span>**-y**  
抑制、 **(はい/いいえ)** プロンプト。 このオプションを使用しない場合、「?」で求め AgeStore すべてのファイルを削除する前に確認します。

<span id="_______-_______"></span> **-?**   
AgeStore コマンドラインのヘルプを表示します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

AgeStore ツールの詳細については、次を参照してください。[を使用して AgeStore](using-agestore.md)します。

 

 





