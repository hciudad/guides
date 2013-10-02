# RoundingWell Database Style Guide

## <a name='TOC'>Table of Contents</a>

  1. [Ids](#ids)  
  1. [Strings](#strings)
  1. [Foreign Keys](#fkeys)

## <a name='ids'>Ids</a>

  - **All Ids are bigint**

## <a name='strings'>Strings</a>

  - **String columns are defined as text unless there is a standard domain-specific length requirement**
  
  (i.e. emails have a max of 320)  
  http://people.planetpostgresql.org/dfetter/index.php?/archives/24-VARCHARn-Considered-Harmful.html  
  and counter argument: http://www.postgresonline.com/journal/archives/154-In-Defense-of-varcharx.html
  
## <a name='fkeys'>Foreign Keys</a>

All foreign keys are on delete restrict UNLESS the rows in question are absolutely senseless without 
the parent table entry (i.e. security question rows for a user are on delete cascade)
