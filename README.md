# Conditional Pipeline Lab

Практическая лабораторная работа по AWS CodePipeline, CodeBuild и GitHub.

## Цель

Понять, как работает conditional execution в CI/CD pipeline.

Pipeline должен:

- выполнять build/test для всех веток  
- НЕ выполнять deploy для feature веток  
- выполнять deploy только для main  
- требовать manual approval перед deploy  

---

## Используемые сервисы

- GitHub  
- AWS CodeBuild  
- AWS CodePipeline  
- SSH / EC2  

---

## Структура проекта

app.txt  
buildspec.yml  
README.md  

---

## Логика conditional execution

В файле `buildspec.yml`:

if echo "$CODEBUILD_WEBHOOK_HEAD_REF" | grep -q "main"; then  
  echo "MAIN branch → deploy allowed"  
else  
  echo "NOT main → deploy skipped"  
fi  

---

## Поведение pipeline

### Feature branch (feature/test)

Результат:

NOT main → deploy skipped  

👉 deploy НЕ выполняется

---

### Main branch

Результат:

MAIN branch → deploy allowed  

👉 pipeline может идти дальше

---

## Архитектура pipeline

Source → Build → Approval → Deploy  

---

## Manual Approval

Перед deploy используется:

- Manual approval stage  
- pipeline останавливается  
- человек принимает решение  

---

## Ключевая идея

В AWS нет обычного `if` в pipeline.

Conditional execution делается через:

- branch (ветки)  
- manual approval (человек)  
- success/failure стадий  
- buildspec logic  
- архитектуру pipeline  

---

## Вывод

Этот проект показывает реальную CI/CD логику:

- pipeline может "принимать решения"  
- feature ветки не идут в production  
- production требует подтверждения  
- логика может быть вынесена в buildspec  

---

## Next Steps

- Deploy на S3  
- Deploy на EC2  
- Полноценный production pipeline (DevOps Pro уровень)
