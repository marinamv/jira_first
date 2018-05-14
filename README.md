# jira_first

feedback:
вот небольшой фидбек:
- логирование +
- наличие readme файла +
- методы которые возвращают boolean результат +, мало кто так сделал
public boolean isIssueDescriptionCorrect(String description) {
        return waitToBePresentAndContainsText(issueDescriptionLocator, description);
    }


- помню, что ты говорила, что сделала 2-е задание частично, но на всякий случай укажу, что hostURL = new URL("
http://127.0.0.1:4444/wd/hub"
); адрес надо вынести в проперти



- поля пропертей можно сделать константами либо энум  result.put("JiraUrl", propertyFileValues.getProperty("JiraUrl"));



- setBrowserName("firefox" ); перечень браузеров можно вынести в enum


- тут судя по всему забыла удалить - By buttonSelector = btnBugOpened;
public boolean isBugOpenedBtnPresent() {
        By buttonSelector = btnBugOpened;
        try {
            driver.findElement(buttonSelector);


- подобный метод можно было сделать один общий для всех в хелпере, чтобы он принимал локатор, т.к. все эти методы одинаковые внутри 
 public boolean isInProgressBtnPresent() {
        By buttonSelector = btnBugInProgress;
        try {
            driver.findElement(buttonSelector);
            return true;
        } catch (NoSuchElementException e) {
            return false;
        }
    }


- этот метод тоже можно унифицировать, как и ^^^^
public IssuePage clickBugReopenedBtn() {
        waitTillBeAbleToClick(btnBugReopened);
        return this;
- public IssuePage robot() хорошо бы назвать более понятно, что он делает (selectItem)


- можно изменить путь инициализации локаторов, тогда не надо будет каждый раз дергать драйвер. Например если использовать такой вариант:
@FindBy(id = "project-field")
private WebElement fieldProjectLocator;
то можно будет делать такой вызов 
fieldProjectLocator.clear(); - что сделает код более читабельным
вместо 
driver.findElement(fieldProjectLocator).clear(); 

- в RemoteWebDriverFactory, лучше использовать  switch case, будет лучше выглядеть


- ассершены без дескрипшена assertEquals(loginPage.isOnThePage(), true); assertTrue(issuePage.isProjectIdCorrect(project));


- коментарии в коде +, но если надо делать какое-то действие только для определенного браузера, лучше добавить условие для этого, чтобы выполнялось только по необходимости
.switchDescriptionToTextMode() // this step is for Chrome - it can't focus on description if it's in visual mode


- в тесте с загрузкой файла, у тебя всегда используется один и тот же тикет, это не правильно. Логичнее использовать тикет который ты создала до этого (раз уж у тебя тесты зависят друг от друга)


- checkBugWorkflow и checkStoryWorkflow довольно длинные и имеют много ассершенов (без описания), хорошо бы разделить на несколько тестов для проверки каждого статуса
