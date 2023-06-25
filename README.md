# Gist-Chameleon
gist for Chameleon


import React, { useState, useEffect } from 'react';
import { httpGet, httpPatch } from 'lib/http';

export const Dropdown = ({ buttonText }) => {
  const [isOpen, setIsOpen] = useState(false);

  useEffect(() => {
    httpGet(`users/${userId}`).then((user) => {
      setIsOpen(user[`dropdown_${name}`]);
    });
  }, []);

  const onToggle = () => {
    setIsOpen(!isOpen);
  };

  return (
    <>
      <div className="dropdown">
        <button
          type="button"
          className="dropdown-button"
          id="dropdownButton"
          aria-haspopup="true"
          aria-expanded={isOpen}
          onClick={onToggle}
        >
          {buttonText}
        </button>

        <ul className={`${isOpen ? 'dropdown-open' : ''} dropdown-menu dropdown-section`} aria-labelledby="dropdownButton" role="menu">
          <DropdownSection title="Items">
            <a href="/page1">Page 1</a>
            <DropdownItem href="/page2">Page 2</DropdownItem>
            <DropdownItem href="/page3">Page 3</DropdownItem>
            <DropdownItem href="/page4">Page 4</DropdownItem>
          </DropdownSection>
        </ul>

        <ul className={`${isOpen ? 'dropdown-open' : ''} dropdown-menu dropdown-section`}>
          <DropdownSection title="More items">
            <DropdownItem href="/page5">Page 5</DropdownItem>
            <DropdownItem href="/page9">Page 9</DropdownItem>
          </DropdownSection>
        </ul>
      </div>
    </>
  );
};

const DropdownSection = ({ title, children }) => {
  return (
    <>
      <div>{title}</div>
      {children}
    </>
  );
};

const DropdownItem = ({ href, children }) => {
  const onItemSelect = () => {
    httpPatch('user', { [`menu-state-${key}`]: true });
    // Perform additional actions if needed
  };

  return (
    <li>
      <a href={href} onClick={onItemSelect}>
        {children}
      </a>
    </li>
  );
};

window.currentUser = { id: '19', name: 'Jane', email: 'jane@chameleon.io' };

export const ActiveProfiles = ({ profiles, onLaunchProfile }) => {
  const activeProfiles = profiles.filter(
    (profile) =>
      !profile.disabled && new Date(profile.last_seen_time) > new Date(new Date().getTime() - 24 * 60 * 1000)
  );

  if (activeProfiles.length === 1 && activeProfiles[0].email === window.currentUser.email) {
    activeProfiles.length = 0;
  }

  return (
    <div>
      {activeProfiles.map((profile) => (
        <div onClick={() => onLaunchProfile(profile.name, profile.email)}>
          {profile.name} - {profile.email}
        </div>
      ))}
    </div>
  );
};


Here is the updated formate , where there were a few errors including a missing href link, a missing callback function on the item dropdown button, some typos and so forth.
