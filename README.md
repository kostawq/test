# test
Создал функцию в отдельном классе в либе CCprintService
QString correctSymbolsInMessage(QString str)
{
  QString correctSymbols("\n .,-?!'\":/\\№()N=ёЁ")
  for(quin16 i = 0; i< str.length(); i++)
  {
    Qchar s = str.at(i);
    if(s>=0x30 && s<=39 || s=0xa)
    {
      continue;
    }
    if(correctSymbols.contains(s))
    {
      continue;
    }
    if(s<0x410 || s>0x44f)
    {
      str[i] = ' ';
    }
  }
}

В классах где создаются view (inrecordView.. out.. sb) обернул все поля в неё
{
...
m_modeUsage = Tools::correctSymbolsInMessage(model.create....)
...
if(needToPrint(data.m_msgData.m_type, data.m_msgData.m_mode))
{
  m_pch = correctSymbolsInMessage(.....)
}
else
{
  m_pch = "-"
}
........
}

в inrecordView.cpp сделал функцию
bool needToPrint(inmshTypeWrapper::inMsgType type, inmshTypeWrapper::inMsgType mode)
{
  if((type == FS || type == code) && mode !=duplicate && mode !=alien)
  {
  return true
  }
  return false
}
